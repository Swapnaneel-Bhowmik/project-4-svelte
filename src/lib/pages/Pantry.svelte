<script>
  let {onBack} = $props();

  import PantryInventory from "../PantryInventory.svelte";

  let pantry = $state([]);

  function addPantryItem(i) {
    pantry = [i, ...pantry];
  }
  function updatePantry(i) {
    pantry = pantry.map(p => p.id === i.id ? i : p);
  }
  function removePantry(id) {
    pantry = pantry.filter(i => i.id !== id);
  }
</script>

<!-- Back button fixed -->
<button onclick={onBack}>⬅ Back</button>

<div class="container">
  <PantryInventory
    pantry={pantry}
    onAdd={addPantryItem}
    onUpdate={updatePantry}
    onRemove={removePantry}
  />
</div>

<style>
  :root {
    --primary: #d97706; /* Amber */
    --primary-hover: #b45309;
    --danger: #dc2626;
    --radius: 10px;
    --shadow: 0 4px 12px rgba(0,0,0,0.08);
    --border: #e5e7eb;
    --bg: #f9fafb;
  }

  /* Back button fixed top-left */
  button {
    position: fixed;
    top: 1rem;
    left: 1rem;
    background: none;
    border: none;
    font-size: 1rem;
    padding: 0.4rem 0.6rem;
    cursor: pointer;
    color: var(--primary);
    font-weight: 600;
    border-radius: var(--radius);
    transition: 0.2s ease;
    z-index: 100;
  }

  button:hover {
    background: rgba(217,119,6,0.12);
    color: var(--primary-hover);
  }

  button:active {
    transform: scale(0.96);
  }

  /* Full-page container for two columns */
  .container {
    display: flex;
    width: 100vw;
    height: 100vh;
    gap: 2rem;
    padding: 1.5rem;
    box-sizing: border-box;
    background: var(--bg);
  }

  /* Form on left (from PantryInventory component) */
  .form {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1.5rem;
    border-radius: var(--radius);
    background: white;
    box-shadow: var(--shadow);
    max-height: 100%; /* prevent vertical scroll */
    overflow: hidden;
  }

  /* Pantry list on right */
  .list {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
    overflow-y: auto;
    max-height: 100%;
  }

  /* Mobile responsiveness */
  @media (max-width: 900px) {
    .container {
      flex-direction: column;
      height: auto;
    }

    .list {
      max-height: 300px;
    }
  }
</style>
