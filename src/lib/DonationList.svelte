<script>
  let { donations = [], onUpdate, onDelete } = $props();

  function reserve(d) {
    onUpdate({ ...d, status: "reserved" });
  }
  function complete(d) {
    onUpdate({ ...d, status: "completed" });
  }
</script>

{#if donations.length === 0}
  <p class="empty">No donations yet.</p>
{:else}
  <ul class="list">
    {#each donations as d}
      <li class="item {d.status}">
        <div class="content">
          <strong>{d.item}</strong> — {d.qty}
          {#if d.name} <span class="donor">by {d.name}</span> {/if}
        </div>

        <div class="buttons">
          {#if d.status === "available"}
            <button class="btn reserve" onclick={() => reserve(d)}>Reserve</button>
          {/if}

          {#if d.status === "reserved"}
            <button class="btn complete" onclick={() => complete(d)}>Complete</button>
          {/if}

          <button class="btn delete" onclick={() => onDelete(d.id)}>Delete</button>
        </div>
      </li>
    {/each}
  </ul>
{/if}

<style>
  :root {
    --available: #2b8a3e;
    --reserved: #d97706;
    --completed: #2563eb;
    --delete: #dc2626;
    --radius: 8px;
    --shadow: 0 3px 8px rgba(0,0,0,0.05);
  }

  .empty {
    padding: 1rem;
    text-align: center;
    color: #666;
    font-style: italic;
  }

  .list {
    padding: 0;
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 0.9rem;
  }

  .item {
    padding: 1rem 1.2rem;
    border: 1px solid #eee;
    border-radius: var(--radius);
    background: white;
    box-shadow: var(--shadow);
    display: flex;
    flex-direction: column;
    gap: 0.6rem;
    transition: 0.2s ease;
    animation: fadeIn 0.25s ease;
  }

  .item:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 12px rgba(0,0,0,0.1);
  }

  /* Status-color left border */
  .item.available {
    border-left: 4px solid var(--available);
  }
  .item.reserved {
    border-left: 4px solid var(--reserved);
  }
  .item.completed {
    border-left: 4px solid var(--completed);
  }

  .content {
    font-size: 1rem;
  }

  .donor {
    color: #555;
    font-style: italic;
    margin-left: 4px;
  }

  /* Buttons container */
  .buttons {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
  }

  /* Base button style */
  .btn {
    padding: 0.45rem 0.75rem;
    border: none;
    border-radius: var(--radius);
    cursor: pointer;
    color: white;
    font-size: 0.9rem;
    font-weight: 600;
    transition: 0.2s ease;
  }

  .btn:hover {
    transform: translateY(-2px);
    opacity: 0.9;
  }

  .btn:active {
    transform: scale(0.95);
  }

  /* Status button colors */
  .reserve { background: var(--reserved); }
  .complete { background: var(--completed); }
  .delete { background: var(--delete); }

  /* Smooth fade animation */
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(4px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @media (max-width: 600px) {
    .item {
      padding: 0.9rem;
    }
    .btn {
      font-size: 0.85rem;
      padding: 0.4rem 0.7rem;
    }
  }
</style>
