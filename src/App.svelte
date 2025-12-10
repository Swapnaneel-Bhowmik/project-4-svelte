<script>
  import Donations from "./lib/pages/Donations.svelte";
  import Volunteers from "./lib/pages/Volunteers.svelte";
  import Pantry from "./lib/pages/Pantry.svelte";

  let page = $state("home");

  function go(p) {
    page = p;
  }
</script>

<main>
  {#if page === "home"}
    <div class="card home-card">
      <h1>Community Food Prototype</h1>

      <div class="nav-buttons">
        <button onclick={() => go("donations")}>🍎 Food Donations</button>
        <button onclick={() => go("volunteers")}>🤝 Volunteer Signup</button>
        <button onclick={() => go("pantry")}>📦 Pantry Inventory</button>
      </div>
    </div>

  {:else if page === "donations"}
    <Donations onBack={() => go("home")} />

  {:else if page === "volunteers"}
    <Volunteers onBack={() => go("home")} />

  {:else if page === "pantry"}
    <Pantry onBack={() => go("home")} />
  {/if}
</main>

<style>
  :root {
    --bg: #fafafa;
    --text: #222;
    --primary: #2563eb;
    --primary-hover: #1e4fcc;
    --radius: 10px;
    --shadow: 0 4px 12px rgba(0,0,0,0.08);
  }

  main {
    width: 100vw;
    height: 100vh;
    padding: 2rem;
    font-family: system-ui, sans-serif;
    background: var(--bg);
    color: var(--text);
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
  }

  /* Card container */
  .card {
    background: white;
    padding: 2rem;
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    text-align: center;
    animation: fadeIn 0.4s ease;
    width: 100%;
    max-width: 400px;
  }

  h1 {
    margin-bottom: 1.5rem;
    font-size: 2rem;
    font-weight: 700;
  }

  /* Navigation buttons container */
  .nav-buttons {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 1rem;
  }

  /* Buttons */
  button {
    padding: 0.9rem 1.2rem;
    font-size: 1.1rem;
    border-radius: var(--radius);
    border: none;
    cursor: pointer;
    background: var(--primary);
    color: white;
    transition: all 0.2s ease;
    box-shadow: var(--shadow);
  }

  button:hover {
    background: var(--primary-hover);
    transform: translateY(-2px);
    box-shadow: 0 6px 14px rgba(0,0,0,0.12);
  }

  button:active {
    transform: translateY(0);
    box-shadow: var(--shadow);
  }

  /* Smooth Fade animation */
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(6px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* Mobile */
  @media (max-width: 600px) {
    main {
      padding: 1rem;
    }
    .card {
      padding: 1.5rem;
      max-width: 100%;
    }
    button {
      font-size: 1rem;
      padding: 0.8rem;
    }
  }
</style>
