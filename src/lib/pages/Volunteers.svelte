<script>
  let {onBack} = $props();

  import VolunteerSignup from "../VolunteerSignup.svelte";

  let volunteers = $state([]);

  function addVolunteer(v) {
    volunteers = [v, ...volunteers];
  }

  function removeVolunteer(id) {
    volunteers = volunteers.filter(v => v.id !== id);
  }
</script>

<button onclick={onBack}>⬅ Back</button>

<div class="card">
    <h2>Volunteer Signup</h2>

    <VolunteerSignup
    volunteers={volunteers}
    onAdd={addVolunteer}
    onRemove={removeVolunteer}
    />
</div>

<style>
  :root {
    --bg: #fafafa;
    --text: #222;
    --primary: #0d9488; /* Teal for volunteers */
    --primary-hover: #0b7d73;
    --radius: 8px;
    --shadow: 0 4px 12px rgba(0,0,0,0.08);
  }

  /* Back button */
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
    z-index: 100; /* ensure it stays above content */
  }

  button:hover {
    background: rgba(13, 148, 136, 0.12);
    color: var(--primary-hover);
  }

  button:active {
    transform: scale(0.96);
  }

  /* Card container */
  .card {
    background: white;
    padding: 1.5rem;
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    animation: fadeIn 0.35s ease;
  }

  /* Title styling */
  h2 {
    margin: 1rem 0 1.5rem;
    font-size: 1.8rem;
    font-weight: 700;
    color: var(--text);
  }

  /* Fade animation */
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(6px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* Mobile styles */
  @media (max-width: 600px) {
    .card {
      padding: 1rem;
    }
    h2 {
      font-size: 1.5rem;
    }
  }
</style>
