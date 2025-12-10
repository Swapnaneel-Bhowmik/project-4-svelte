<script>
  let {volunteers = [], onAdd, onRemove} = $props();

  let name = $state("");
  let contact = $state("");

  function handleSubmit(event) {
    event.preventDefault();
    if (!name || !contact) return;

    onAdd({
      id: crypto.randomUUID?.() ?? Math.random().toString(36).slice(2),
      name,
      contact
    });

    name = "";
    contact = "";
  }
</script>

<div class="container">

  <!-- Left Column: Form -->
  <form onsubmit={handleSubmit} class="card form">
    <h2>Volunteer Signup</h2>
    <input placeholder="Name" bind:value={name} required />
    <input placeholder="Contact" bind:value={contact} required />
    <button type="submit" class="submit-btn">
      <!-- Icon: user-plus -->
      <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="currentColor">
        <path d="M16 14v-2h-2V10h2V8h2v2h2v2h-2v2h-2zm-8 2a4 4 0 1 0-4-4 4 4 0 0 0 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
      </svg>
      Add Volunteer
    </button>
  </form>

  <!-- Right Column: List -->
  <ul class="vol-list">
    {#each volunteers as v}
      <li class="vol-item">
        <div class="info">
          <strong>{v.name}</strong>
          <span class="contact">{v.contact}</span>
        </div>
        <button class="remove-btn" onclick={() => onRemove(v.id)}>
          <!-- Trash icon -->
          <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="currentColor">
            <path d="M3 6h18v2H3V6zm2 3h14l-1.5 12.5a1 1 0 0 1-1 .5H7.5a1 1 0 0 1-1-.5L5 9z"/>
          </svg>
          Remove
        </button>
      </li>
    {/each}
  </ul>

</div>

<style>
  :root {
  --primary: #0d9488; /* teal */
  --primary-hover: #0a7a70;
  --danger: #dc2626;
  --radius: 10px;
  --shadow: 0 4px 12px rgba(0,0,0,0.08);
  --border: #e5e7eb;
  --bg: #f9fafb;
}

/* --- Full Page Layout --- */
.container {
  display: flex;
  width: 100vw;
  height: 100vh;
  background: var(--bg);
  padding: 1.5rem;
  box-sizing: border-box;
  gap: 2rem;
}

/* Left column (form) */
.form {
  flex: 1.3; /* slightly wider */
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 1.5rem;
  border-radius: var(--radius);
  background: white;
  box-shadow: var(--shadow);
  overflow: hidden; /* prevent vertical scroll */
  box-sizing: border-box;
}

.form h2 {
  margin-bottom: 0.5rem;
  font-size: 1.4rem;
  color: var(--primary);
}

input {
  padding: 0.7rem 1rem;
  border-radius: var(--radius);
  border: 1px solid #d1d5db;
  font-size: 1rem;
  transition: 0.2s;
  width: 100%;
  box-sizing: border-box;
}

input:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(13,148,136,0.25);
}

.submit-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  justify-content: center;
  padding: 0.75rem;
  background: var(--primary);
  color: white;
  font-size: 1rem;
  border-radius: var(--radius);
  border: none;
  cursor: pointer;
  font-weight: 600;
  transition: 0.2s ease;
}

.submit-btn:hover {
  background: var(--primary-hover);
  transform: translateY(-2px);
  box-shadow: 0 6px 14px rgba(0,0,0,0.12);
}

/* Icon inside button */
.icon {
  width: 1.2rem;
  height: 1.2rem;
}

/* Right column (scrollable list) */
.vol-list {
  flex: 1.7;
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 0.9rem;
  overflow-y: auto;
  max-height: 100%;
  box-sizing: border-box;
}

.vol-item {
  padding: 1rem;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: var(--shadow);
  transition: 0.2s ease;
}

.vol-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 14px rgba(0,0,0,0.1);
}

.info {
  display: flex;
  flex-direction: column;
}

.contact {
  font-size: 0.9rem;
  color: #555;
}

.remove-btn {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  background: var(--danger);
  color: white;
  border: none;
  padding: 0.45rem 0.8rem;
  border-radius: var(--radius);
  cursor: pointer;
  font-weight: 600;
  transition: 0.2s ease;
}

.remove-btn:hover {
  opacity: 0.9;
  transform: translateY(-1px);
}

/* Scrollbar styling */
.vol-list::-webkit-scrollbar {
  width: 8px;
}

.vol-list::-webkit-scrollbar-thumb {
  background-color: #cbd5e1;
  border-radius: 4px;
}

/* Mobile adjustments */
@media (max-width: 900px) {
  .container {
    flex-direction: column;
    height: auto;
  }

  .form {
    width: 100%;
  }

  .vol-list {
    max-height: 300px;
  }
}

</style>
