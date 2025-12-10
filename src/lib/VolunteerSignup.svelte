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

<form onsubmit={handleSubmit} class="card">
  <input placeholder="Name" bind:value={name} required />
  <input placeholder="Contact" bind:value={contact} required />
  <button type="submit">Volunteer</button>
</form>

<ul class="vol-list">
  {#each volunteers as v}
    <li class="vol-item">
      {v.name} — {v.contact}
      <button onclick={() => onRemove(v.id)}>Remove</button>
    </li>
  {/each}
</ul>

<style>
  .card { display:flex; flex-direction:column; gap:.5rem; padding:1rem; border:1px solid #ddd; border-radius:8px; }
  .vol-list { list-style:none; padding:0; margin-top:1rem; display:flex; flex-direction:column; gap:.5rem; }
  .vol-item { border:1px solid #eaeaea; padding:.5rem; border-radius:6px; display:flex; justify-content:space-between; }
</style>
