<script lang="ts">
  // ---- Types ----
  type Zone = 'exec' | 'communications' | 'membership' | 'program' | 'finance';

  type Officer = {
    name: string;
    role: string;
    photo?: string;      // filename in /headshots (e.g., 'josh.JPG')
    zone: Zone;
    linkedin?: string;   // add 'https://...' to enable the link
  };

  // ---- DATA: fill in linkedin URLs whenever you have them ----
  const execBoard: Officer[] = [
    { name: 'Joshua Chikosha', role: 'President', photo: 'josh.JPG', zone: 'exec' /*, linkedin: ''*/ },
    { name: 'Kilali Latter', role: 'Vice-President', photo: 'kilali.JPG', zone: 'exec' /*, linkedin: ''*/ },
    { name: 'Angela Kamgang', role: 'Treasurer', photo: 'angela.JPG', zone: 'exec' /*, linkedin: ''*/ },
    { name: 'David Udoh', role: 'Programs Chair', photo: 'david.JPG', zone: 'exec' /*, linkedin: ''*/ },
    { name: 'Enow Tanyi', role: 'Secretary', photo: 'enow.JPG', zone: 'exec' /*, linkedin: ''*/ }
  ];

  const communications: Officer[] = [
    { name: 'Tobi Sakin', role: 'Cockrell Relations Chair', photo: 'tobi.JPG', zone: 'communications' },
    { name: 'Kevin Uduji', role: 'Telecommunications Chair', zone: 'communications' },
    { name: 'Casey Hawthorne', role: 'Public Relations Chair', photo: 'casey.JPG', zone: 'communications' },
    { name: 'Aaron Evans', role: 'Public Relations Chair', photo: 'aaron.JPG', zone: 'communications' },
    { name: 'Benita Egorah', role: 'Public Relations Chair', photo: 'benita.JPG', zone: 'communications' },
    { name: 'Giles Mbakwa', role: 'Public Relations Chair', photo: 'giles.JPG', zone: 'communications' }
  ];

  const membership: Officer[] = [
    { name: 'Chinoso Nwanebi', role: 'Membership Chair', photo: 'chinoso.JPG', zone: 'membership' },
    { name: 'Sara Adio', role: 'Membership Chair', photo: 'sara.JPG', zone: 'membership' },
    { name: 'Alexia Mougoue', role: 'FAT Advisor', photo: 'alexia.JPG', zone: 'membership' },
    { name: 'Laci Moline', role: 'BWISE Chair', photo: 'laci.JPG', zone: 'membership' },
    { name: 'Chancellor Joseph', role: 'Professional Development Chair', zone: 'membership' },
    { name: 'Kofi Bekoe', role: 'Academic Excellence Chair', photo: 'kofi.JPG', zone: 'membership' },
    { name: 'Adam Mann', role: 'Graduate Liaison', zone: 'membership' }
  ];

  const program: Officer[] = [
    { name: 'Ganiat Ogidan', role: 'Conference Planner', zone: 'program' },
    { name: 'Jaydon Anyikam', role: 'Conference Planner', photo: 'jaydon.JPG', zone: 'program' },
    { name: 'Terrence Adegbesan', role: 'Finance Chair', photo: 'terrence.JPG', zone: 'program' },
    { name: 'Victor Uche', role: 'Corporate Liaison', photo: 'victor.JPG', zone: 'program' },
    { name: 'Christine Daniel', role: 'Fundraising Chair', photo: 'christine.JPG', zone: 'program' }
  ];

  const finance: Officer[] = [
    { name: 'Alexander Milton', role: 'Athletics Chair', photo: 'alex.JPG', zone: 'finance' },
    { name: 'Imuetiyan Ogbeide', role: 'Pre-Collegiate Initiative Chair', photo: 'Imuetiyan.JPG', zone: 'finance' },
    { name: 'Jaylon Collins', role: 'TORCH Chair', photo: 'jaylon.JPG', zone: 'finance' },
    { name: 'Stephanie Ohuakanwa', role: 'Social Chair', zone: 'finance' },
    { name: 'Tee Edwards', role: 'Social Chair', zone: 'finance' }
  ];

  // ---- ZONE GROUPS ----
  const zones: { id: Zone; title: string; people: Officer[] }[] = [
    { id: 'communications', title: 'Communications Zone', people: communications },
    { id: 'membership',     title: 'Membership Zone',     people: membership },
    { id: 'program',        title: 'Program Zone',        people: program },
    { id: 'finance',        title: 'Finance Zone',        people: finance }
  ];

  // ---- COLORS ----
  const zoneColors: Record<Zone, { stripe: string; chip: string }> = {
    exec:           { stripe: '#FFB400', chip: '#FFB400' }, // gold
    communications: { stripe: '#98B5E0', chip: '#D6E3F8' }, // blue
    membership:     { stripe: '#E39AA0', chip: '#F6D3D6' }, // red
    program:        { stripe: '#AACB97', chip: '#DAECD0' }, // green
    finance:        { stripe: '#E8D17A', chip: '#F7EFC0' }  // yellow
  };

  // ---- HELPERS ----
  const photoPath = (p?: string) => (p ? `/headshots/${p}` : '/icons/avatar-placeholder.png');
  const onImgError = (e: Event) => {
    const t = e.currentTarget as HTMLImageElement;
    t.src = '/icons/avatar-placeholder.png';
  };
</script>

<section class="officers">
  <!-- Exec Board (prominent) -->
  <h1>25-26 Top Five</h1>
  <div class="grid exec">
    {#each execBoard as o}
      <article
        class="card"
        data-zone="exec"
        style={`--stripe:${zoneColors[o.zone].stripe}; --chip:${zoneColors[o.zone].chip};`}
      >
        <div class="photo">
          <img src={photoPath(o.photo)} alt={`${o.name} headshot`} on:error={onImgError} />
        </div>
        <div class="meta">
          <h3>{o.name}</h3>
          <p class="role"><span class="chip">{o.role}</span></p>
        </div>
        <div class="links">
          <!-- Always an <a>. Add linkedin in the data above to enable it -->
          <a
            href={o.linkedin ?? '#'}
            class:disabled={!o.linkedin}
            aria-label={`LinkedIn: ${o.name}`}
            rel={o.linkedin ? 'noopener noreferrer' : undefined}
            target={o.linkedin ? '_blank' : undefined}
          >
            <img src="/icons/linkedin.png" alt="LinkedIn" />
          </a>
        </div>
      </article>
    {/each}
  </div>

  <!-- Other Zones -->
  {#each zones as z}
    <h2>{z.title}</h2>
    <div class="grid" data-zone={z.id}>
      {#each z.people as o}
        <article
          class="card"
          data-zone={o.zone}
          style={`--stripe:${zoneColors[o.zone].stripe}; --chip:${zoneColors[o.zone].chip};`}
        >
          <div class="photo">
            <img src={photoPath(o.photo)} alt={`${o.name} headshot`} on:error={onImgError} />
          </div>
          <div class="meta">
            <h3>{o.name}</h3>
            <p class="role"><span class="chip">{o.role}</span></p>
          </div>
          <div class="links">
            <a
              href={o.linkedin ?? '#'}
              class:disabled={!o.linkedin}
              aria-label={`LinkedIn: ${o.name}`}
              rel={o.linkedin ? 'noopener noreferrer' : undefined}
              target={o.linkedin ? '_blank' : undefined}
            >
              <img src="/icons/linkedin.png" alt="LinkedIn" />
            </a>
          </div>
        </article>
      {/each}
    </div>
  {/each}
</section>

<style lang="scss">
/* Page shell */
.officers {
  padding: 7rem 1.25rem 3rem; /* account for fixed navbar */
  max-width: 1100px;
  margin-inline: auto;
  color: #000;
}

/* Headings */
h1 {
  text-align: center;
  font-size: clamp(1.8rem, 3.8vw, 2.5rem);
  margin-bottom: 1.25rem;
}
h2 {
  font-size: clamp(1.2rem, 2.5vw, 1.6rem);
  margin: 3rem 0 1rem;
  color: #333;
}

/* Shared grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 1rem;
  justify-items: center;
  align-items: start;
  padding-inline: 0.5rem;
}

/* Exec row: larger cards & centered layout */
.grid.exec {
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  justify-content: center;
  margin-bottom: 2.5rem;
}

/* Card */
.card {
  position: relative;
  background: #fff;
  border: 1px solid #E5D9B8; /* sand border */
  border-radius: 1rem;
  overflow: hidden;
  display: grid;
  grid-template-rows: auto 1fr auto;
  width: 100%;
  max-width: 360px;
  box-shadow: 0 2px 6px rgba(0,0,0,.04);
}

/* Exec emphasis */
.card[data-zone="exec"] {
  transform: scale(1.03);
  border-width: 2px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.08);
}

/* Zone stripe */
.card::before {
  content: "";
  position: absolute;
  inset: 0 0 auto 0;
  height: 6px;
  background: var(--stripe);
}

/* Photo */
.photo {
  aspect-ratio: 4 / 3;
  background: #f7f3e4;
  display: flex;
  align-items: center;
  justify-content: center;
}
.photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 0.5rem;
}

/* Meta */
.meta { padding: 0.85rem 0.95rem 0.35rem; }
.meta h3 { margin: 0; font-size: 1.08rem; line-height: 1.25; }
.meta .role { margin: 0.45rem 0 0.6rem; }
.chip {
  display: inline-block;
  background: var(--chip);
  padding: 0.3rem 0.55rem;
  border-radius: 999px;
  font-size: 0.82rem;
}

/* Links */
.links {
  padding: 0.65rem 0.95rem 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.links img { width: 22px; height: 22px; object-fit: contain; }
.links a.disabled {
  opacity: 0.35;
  pointer-events: none;
}

/* Small screens */
@media (max-width: 480px) {
  .officers { padding-top: 6.5rem; }
  .grid { gap: 0.75rem; }
}
</style>