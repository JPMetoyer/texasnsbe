<script lang="ts">
  import { onMount } from 'svelte';

  type Member = {
    name: string;
    points: number;
  };

  // You can override this when using the component if the URL changes
  export let csvUrl =
    'https://docs.google.com/spreadsheets/d/e/2PACX-1vSTl6ZBQ_6Hx-OFZaK3hCVkBa4zqM-oRuwlO_bPZx7so8sMOjjPN5YAN_VV_oZs2tJERWWrYsvAQL8G/pub?output=csv';

  let members: Member[] = [];
  let loading = true;
  let error: string | null = null;
  let query = '';

  onMount(async () => {
    try {
      const res = await fetch(csvUrl);
      if (!res.ok) throw new Error('Failed to load leaderboard');

      const text = await res.text();
      members = parseCsv(text);
    } catch (e: any) {
      console.error(e);
      error = 'Unable to load leaderboard right now.';
    } finally {
      loading = false;
    }
  });

  function parseCsv(text: string): Member[] {
    const lines = text.trim().split(/\r?\n/);

    if (lines.length < 3) return [];

    // Row 1 is usually blank, row 2 (index 1) contains the headers
    const headerLine = lines[1];
    const headers = headerLine.split(',');

    // Try to locate the "Final Total" column explicitly
    let pointsIdx = headers.findIndex((h) => h.trim().toLowerCase().startsWith('final total'));

    // Fallback: if not found, use the last non-empty header
    if (pointsIdx === -1) {
      for (let i = headers.length - 1; i >= 0; i--) {
        if (headers[i].trim() !== '') {
          pointsIdx = i;
          break;
        }
      }
    }

    if (pointsIdx === -1) pointsIdx = headers.length - 1;

    // First data row is row 3 (index 2)
    const dataLines = lines.slice(2);

    const parsed: Member[] = dataLines
      .map((line) => {
        if (!line.trim()) return null;
        const cols = line.split(',');

        const name = cols[0]?.trim() ?? '';
        const rawPoints = cols[pointsIdx] ?? '0';
        const points = Number(rawPoints) || 0;

        if (!name) return null;
        return { name, points };
      })
      .filter((m): m is Member => m !== null)
      .sort((a, b) => b.points - a.points);

    return parsed;
  }

  $: filtered = members.filter((m) => {
    if (!query) return true;
    const q = query.toLowerCase();
    return m.name.toLowerCase().includes(q);
  });
</script>

<section class="leaderboard-section" aria-label="NSBE Member Leaderboard">
  <div class="inner">
    <header class="heading">
      <p class="eyebrow">Most active members!</p>
      <h2>Leaderboard</h2>
    </header>

    <div class="card">
      <h3>NSBE Leaderboard</h3>

      <div class="search-wrap">
        <input
          type="text"
          bind:value={query}
          placeholder="Search for members..."
          aria-label="Search members by name"
        />
      </div>

      {#if loading}
        <div class="status">Loading leaderboard…</div>
      {:else if error}
        <div class="status error">{error}</div>
      {:else}
        <div class="table-wrap">
          <table>
            <thead>
              <tr>
                <th>Rank</th>
                <th>Name</th>
                <th>Points</th>
              </tr>
            </thead>
            <tbody>
              {#if filtered.length === 0}
                <tr>
                  <td colspan="3" class="empty">No members found.</td>
                </tr>
              {:else}
                {#each filtered as m, i}
                  <tr>
                    <td>{i + 1}</td>
                    <td>{m.name}</td>
                    <td>{m.points}</td>
                  </tr>
                {/each}
              {/if}
            </tbody>
          </table>
        </div>
      {/if}
    </div>
  </div>
</section>

<style lang="scss">
.leaderboard-section {
  padding: 3.5rem 1rem 4rem;
  background:
    radial-gradient(circle at 1px 1px, rgba(0, 0, 0, 0.04) 1px, transparent 1px)
      repeat,
    linear-gradient(180deg, #f4eed7 0%, #fdf9ee 100%);
  background-size: 22px 22px, auto;
  display: flex;
  justify-content: center;
}

.inner {
  max-width: 1200px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* Heading */
.heading {
  text-align: center;
  margin-bottom: 1.75rem;

  .eyebrow {
    margin: 0 0 0.35rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.14em;
    font-size: clamp(1rem, 2.1vw, 1.4rem);
    color: #b5651d;
  }

  h2 {
    margin: 0;
    font-size: clamp(2.4rem, 5vw, 3.5rem);
    font-weight: 900;
    text-transform: none;
    letter-spacing: 0.08em;
    color: #000000;
    font-family: 'Rubik', system-ui, -apple-system, BlinkMacSystemFont,
      'Segoe UI', sans-serif;
  }
}

/* Card */
.card {
  width: 100%;
  max-width: 900px;
  border-radius: 1.5rem;
  background: #ffffff;
  border: 1px solid #e5d9b8;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.12);
  padding: 1.75rem 1.5rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.card h3 {
  margin: 0;
  text-align: center;
  font-size: 1.4rem;
  font-weight: 800;
  color: #333333;
}

/* Search */
.search-wrap {
  display: flex;
  justify-content: center;
}

.search-wrap input {
  width: 100%;
  max-width: 420px;
  border-radius: 999px;
  border: 2px solid #b5651d;
  padding: 0.55rem 0.9rem;
  font-size: 0.95rem;
  outline: none;
}

.search-wrap input:focus {
  box-shadow: 0 0 0 2px rgba(181, 101, 29, 0.25);
}

/* Status messages */
.status {
  text-align: center;
  padding: 1rem 0;
  color: #374151;
}

.status.error {
  color: #b91c1c;
}

/* Table */
.table-wrap {
  border-radius: 1rem;
  overflow: auto;
  max-height: 400px;
  border: 1px solid #e5e7eb;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.95rem;
}

thead {
  position: sticky;
  top: 0;
  z-index: 1;
}

th,
td {
  padding: 0.55rem 0.75rem;
  text-align: left;
}

thead th {
  background: #e5d9b8;
  color: #000000;
  font-weight: 700;
}

tbody tr:nth-child(even) td {
  background: #f9fafb;
}

tbody tr:nth-child(odd) td {
  background: #ffffff;
}

td:first-child {
  width: 60px;
}

.empty {
  text-align: center;
}

/* Hover effect on desktop */
@media (hover: hover) and (pointer: fine) {
  .card {
    transition: transform 0.25s ease-out;
  }

  .card:hover {
    transform: translateY(-2px);
  }
}

/* Mobile tweaks */
@media (max-width: 640px) {
  .leaderboard-section {
    padding: 3rem 0.75rem 3.25rem;
  }

  .card {
    padding: 1.5rem 1.1rem 1.75rem;
    border-radius: 1.1rem;
  }

  .table-wrap {
    max-height: 320px;
  }
}
</style>