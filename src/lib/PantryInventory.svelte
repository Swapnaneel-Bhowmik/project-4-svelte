<script>
  let {pantry = [], onAdd, onUpdate, onRemove} = $props();

  let name = $state("");
  let qty = $state(1);
  let unit = $state("units");

  function addItem() {
    if (!name) return;
    onAdd({
      id: crypto.randomUUID?.() ?? Math.random().toString(36).slice(2),
      name,
      qty: Number(qty),
      unit
    });
    name = "";
    qty = 1;
  }

  function adjust(item, delta) {
    const updated = { ...item, qty: Math.max(0, item.qty + delta) };
    onUpdate(updated);
  }
</script>

<div class="container">

  <!-- Left: Form -->
  <div class="card form">
    <h2>Pantry Inventory</h2>
    <input placeholder="Item name" bind:value={name} />
    <input type="number" min="1" bind:value={qty} />
    <input placeholder="Unit" bind:value={unit} />
    <button class="submit-btn" onclick={addItem}>
      <!-- Icon: plus-circle -->
      <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="currentColor">
        <path d="M12 5v14m-7-7h14"/>
      </svg>
      Add Item
    </button>
  </div>

  <!-- Right: List -->
  <ul class="list">
    {#each pantry as item}
      <li class="list-item">
        <div class="info">
          <strong>{item.name}</strong>
          <span>{item.qty} {item.unit}</span>
        </div>

        <div class="buttons">
          <button class="btn adjust dec" onclick={() => adjust(item, -1)}>
            <!-- Minus icon -->
            <svg width="50px" height="50px" viewBox="0 0 50 50" xmlns="http://www.w3.org/2000/svg"><path d="M25 42c-9.4 0-17-7.6-17-17S15.6 8 25 8s17 7.6 17 17-7.6 17-17 17zm0-32c-8.3 0-15 6.7-15 15s6.7 15 15 15 15-6.7 15-15-6.7-15-15-15z"/>
              <path d="M16 24h18v2H16z"/>
            </svg>
          </button>
          <button class="btn adjust inc" onclick={() => adjust(item, +1)}>
            <!-- Plus icon -->
            <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="currentColor">
              <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4"/>
            </svg>
          </button>
          <button class="btn remove" onclick={() => onRemove(item.id)}>
            <!-- Trash icon -->
            <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="currentColor">
              <path d="M3 6h18v2H3V6zm2 3h14l-1.5 12.5a1 1 0 0 1-1 .5H7.5a1 1 0 0 1-1-.5L5 9z"/>
            </svg>
          </button>
        </div>
      </li>
    {/each}
  </ul>

</div>

<style>
  :root {
    --primary: #d97706; /* amber */
    --primary-hover: #b45309;
    --danger: #dc2626;
    --radius: 10px;
    --shadow: 0 4px 12px rgba(0,0,0,0.08);
    --border: #e5e7eb;
    --bg: #f9fafb;
  }

  .container {
    display: flex;
    width: 100vw;
    height: 100vh;
    padding: 1.5rem;
    gap: 2rem;
    background: var(--bg);
  }

  .form {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1.5rem;
    border-radius: var(--radius);
    background: white;
    box-shadow: var(--shadow);
  }

  .form h2 { color: var(--primary); }

  input { padding: 0.7rem 1rem; border-radius: var(--radius); border: 1px solid #d1d5db; }
  input:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 3px rgba(217,119,6,0.25); }

  .submit-btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    justify-content: center;
    padding: 0.75rem;
    background: var(--primary);
    color: white;
    border-radius: var(--radius);
    border: none;
    cursor: pointer;
    font-weight: 600;
    transition: 0.2s;
  }
  .submit-btn:hover { background: var(--primary-hover); transform: translateY(-2px); }

  .icon { width: 3.2rem; height: 3.2rem; }

  .list {
    flex: 1;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
  }

  .list-item {
    padding: 1rem;
    border-radius: var(--radius);
    border: 1px solid var(--border);
    background: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: var(--shadow);
  }

  .info { display: flex; flex-direction: column; gap: 0.2rem; }

  .buttons { display: flex; gap: 0.5rem; }

  .btn { display: flex; align-items: center; gap: 0.4rem; padding: 0.45rem 0.7rem; border-radius: var(--radius); border: none; font-weight: 600; cursor: pointer; color: white; transition: 0.2s ease; }

  .adjust.inc { background: var(--primary); }
  .adjust.dec { background: #a16207; }
  .remove { background: var(--danger); }

  .btn:hover { transform: translateY(-1px); }
  .list::-webkit-scrollbar { width: 8px; }
  .list::-webkit-scrollbar-thumb { background-color: #cbd5e1; border-radius: 4px; }

  @media (max-width: 900px) {
    .container { flex-direction: column; height: auto; }
    .list { max-height: 300px; }
  }
</style>
