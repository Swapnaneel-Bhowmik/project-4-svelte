<script>
  let {onAdd} = $props();

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
</script>

<form onsubmit={handleSubmit} class="card">
  <input placeholder="Your name (optional)" bind:value={name} />
  <input placeholder="Item" bind:value={item} required />
  <input type="number" min="1" bind:value={qty} required />
  <button type="submit">Submit Donation</button>
</form>

<style>
  .card { display:flex; flex-direction:column; gap:.5rem; padding:1rem; border:1px solid #ddd; border-radius:8px; }
  input, button { padding: .5rem; border-radius: 6px; border: 1px solid #ccc; }
  button { border: 0; background:#2b8a3e; color:white; }
</style>
