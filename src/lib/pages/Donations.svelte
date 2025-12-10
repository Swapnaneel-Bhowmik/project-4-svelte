<script>
  let {onBack} = $props();

  import DonationForm from "../DonationForm.svelte";
  import DonationList from "../DonationList.svelte";

  let donations = $state([]);

  function addDonation(d) {
    donations = [d, ...donations];
  }
  function updateDonation(updated) {
    donations = donations.map(d => d.id === updated.id ? updated : d);
  }
  function deleteDonation(id) {
    donations = donations.filter(d => d.id !== id);
  }
</script>

<button class="back-btn" onclick={onBack}>⬅ Back</button>

<div class="container">
  <div class="left-column">
    <DonationForm 
      donations={donations}
      onAdd={addDonation}
      onUpdate={updateDonation}
      onDelete={deleteDonation} />
  </div>

  <div class="right-column">
    <DonationList
      donations={donations}
      onUpdate={updateDonation}
      onDelete={deleteDonation} />
  </div>
</div>

<style>
  :root {
    --bg: #fafafa;
    --text: #222;
    --primary: #2563eb;
    --primary-hover: #1e4fcc;
    --radius: 8px;
    --shadow: 0 4px 10px rgba(0,0,0,0.08);
  }

  /* Back button positioned top-left of left column */
.back-btn {
  position: absolute;
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
  z-index: 10;
}

.back-btn:hover {
  background: rgba(37, 99, 235, 0.1);
  color: var(--primary-hover);
}

.back-btn:active {
  transform: scale(0.96);
}

/* Page container */
.container {
  display: flex;
  gap: 1.5rem;
  width: 100%;
  height: calc(100vh - 3rem);
  animation: fadeIn 0.35s ease;
}

/* Left column wider */
.left-column {
  flex: 1.2; /* increased width */
  max-width: 500px; /* optional max width */
  background: white;
  padding: 2rem;
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  overflow-y: auto;
  position: relative; /* for back button */
}

.right-column {
  flex: 1.8; /* adjust proportion */
  background: white;
  padding: 1.5rem;
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  overflow-y: auto;
}

/* Fade animation */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(6px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Mobile adjustments */
@media (max-width: 800px) {
  .container {
    flex-direction: column;
    height: auto;
  }
  .left-column, .right-column {
    max-width: 100%;
  }
  .back-btn {
    position: static;
    margin-bottom: 1rem;
  }
}

</style>
