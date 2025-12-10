<script>
  let {donations = [], onAdd, onUpdate, onDelete} = $props();

  let name = $state("");
  let item = $state("");
  let qty = $state(1);

  function handleSubmit(event) {
    event.preventDefault();
    if (!item || qty <= 0) return;

    onAdd({
      id: crypto.randomUUID?.() ?? Math.random().toString(36).slice(2),
      name,
      item,
      qty,
      status: "available"
    });

    name = "";
    item = "";
    qty = 1;
  }

  function reserve(d) {
    onUpdate({ ...d, status: "reserved" });
  }
  function complete(d) {
    onUpdate({ ...d, status: "completed" });
  }
</script>

<div class="container">

  <!-- Left: Form -->
  <form onsubmit={handleSubmit} class="card form">
    <h2>Food Donations</h2>
    <input placeholder="Your name (optional)" bind:value={name} />
    <input placeholder="Item" bind:value={item} required />
    <input type="number" min="1" bind:value={qty} required />
    <button type="submit" class="submit-btn">
      <!-- Icon: plus-circle -->
      <svg xmlns="http://www.w3.org/2000/svg" class="icon" viewBox="0 0 24 24" fill="currentColor">
        <path d="M12 5v14m-7-7h14"/>
      </svg>
      Add Donation
    </button>
  </form>

  <!-- Right: List -->
  
</div>

<style>
  :root {
    --primary: #2b8a3e;
    --primary-hover: #237231;
    --danger: #dc2626;
    --reserve: #f59e0b;
    --complete: #2563eb;
    --radius: 10px;
    --shadow: 0 4px 12px rgba(0,0,0,0.08);
    --border: #e5e7eb;
    --bg: #f9fafb;
  }

  .container {
    display: flex;
    width: 30vw;
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

  .form h2 {
    color: var(--primary);
  }

  input {
    padding: 0.7rem 1rem;
    border-radius: var(--radius);
    border: 1px solid #d1d5db;
  }

  input:focus {
    outline: none;
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(43,138,62,0.25);
  }

  .submit-btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    justify-content: center;
    padding: 0.75rem;
    background: var(--primary);
    color: white;
    border-radius: var(--radius);
    font-weight: 600;
    cursor: pointer;
    border: none;
    transition: 0.2s;
  }

  .submit-btn:hover { background: var(--primary-hover); transform: translateY(-2px); }

  .icon { width: 1.2rem; height: 1.2rem; }

  .list {
    flex: 1;
    list-style: none;
    padding: 0;
    margin: 0;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 0.9rem;
  }

  .empty { text-align: center; color: #888; }

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
  .status {
    font-size: 0.85rem;
    font-weight: 600;
    text-transform: capitalize;
    color: #555;
  }

  .buttons { display: flex; gap: 0.5rem; }

  .btn { display: flex; align-items: center; gap: 0.4rem; padding: 0.45rem 0.8rem; border-radius: var(--radius); border: none; font-weight: 600; cursor: pointer; color: white; transition: 0.2s ease; }

  .reserve { background: var(--reserve); }
  .reserve:hover { background: #d97706; transform: translateY(-1px); }

  .complete { background: var(--complete); }
  .complete:hover { background: #1e40af; transform: translateY(-1px); }

  .remove { background: var(--danger); }
  .remove:hover { opacity: 0.9; transform: translateY(-1px); }

  .list::-webkit-scrollbar { width: 8px; }
  .list::-webkit-scrollbar-thumb { background-color: #cbd5e1; border-radius: 4px; }

  @media (max-width: 900px) {
    .container { flex-direction: column; height: auto; }
    .list { max-height: 300px; }
  }
</style>
