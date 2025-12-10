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

<div class="card">
  <input placeholder="Item name" bind:value={name} />
  <input type="number" min="1" bind:value={qty} />
  <input placeholder="unit" bind:value={unit} />
  <button onclick={addItem}>Add</button>
</div>

<ul class="list">
  {#each pantry as item}
    <li class="entry">
      <strong>{item.name}</strong> — {item.qty} {item.unit}

      <div class="buttons">
        <button onclick={() => adjust(item, -1)}>-</button>
        <button onclick={() => adjust(item, +1)}>+</button>
        <button onclick={() => onRemove(item.id)}>Remove</button>
      </div>
    </li>
  {/each}
</ul>

<style>
  .card { display:flex; gap:.5rem; flex-direction:column; padding:1rem; border:1px solid #ddd; border-radius:8px; }
  .list { list-style:none; padding:0; margin-top:1rem; display:flex; flex-direction:column; gap:.5rem; }
  .entry { border:1px solid #eee; padding:.5rem; border-radius:6px; display:flex; justify-content:space-between; }
  .buttons button { margin-left:.5rem; }
</style>
