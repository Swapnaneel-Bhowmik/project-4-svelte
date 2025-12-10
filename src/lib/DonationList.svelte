<script>
  let {donations = [], onUpdate, onDelete} = $props();

  function reserve(d) {
    onUpdate({ ...d, status: "reserved" });
  }
  function complete(d) {
    onUpdate({ ...d, status: "completed" });
  }
</script>

{#if donations.length === 0}
  <p>No donations yet.</p>
{:else}
  <ul class="list">
    {#each donations as d}
      <li class="item">
        <strong>{d.item}</strong> — {d.qty}
        {#if d.name} (by {d.name}) {/if}

        <div class="buttons">
          {#if d.status === "available"}
            <button onclick={() => reserve(d)}>Reserve</button>
          {/if}

          {#if d.status === "reserved"}
            <button onclick={() => complete(d)}>Complete</button>
          {/if}

          <button onclick={() => onDelete(d.id)}>Delete</button>
        </div>
      </li>
    {/each}
  </ul>
{/if}

<style>
  .list { padding:0; list-style:none; display:flex; flex-direction:column; gap:.75rem; }
  .item { padding:.75rem; border:1px solid #eee; border-radius:8px; }
  .buttons button { margin-right:.5rem; }
</style>
