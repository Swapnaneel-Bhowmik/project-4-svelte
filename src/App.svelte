<script>
  import DonationForm from "./lib/DonationForm.svelte";
  import DonationList from "./lib/DonationList.svelte";
  import VolunteerSignup from "./lib/VolunteerSignup.svelte";
  import PantryInventory from "./lib/PantryInventory.svelte";

  let donations = $state([]);
  let volunteers = $state([]);
  let pantry = $state([]);

  // Donations
  function addDonation(d) {
    donations = [d, ...donations];
  }
  function updateDonation(updated) {
    donations = donations.map(d => d.id === updated.id ? updated : d);
  }
  function deleteDonation(id) {
    donations = donations.filter(d => d.id !== id);
  }

  // Volunteers
  function addVolunteer(v) {
    volunteers = [v, ...volunteers];
  }
  function removeVolunteer(id) {
    volunteers = volunteers.filter(v => v.id !== id);
  }

  // Pantry
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

<main>
  <h1>Community Food Prototype (Svelte 5)</h1>

  <section>
    <h2>Food Donations</h2>
    <DonationForm onAdd={addDonation} />
    <DonationList
      donations={donations}
      onUpdate={updateDonation}
      onDelete={deleteDonation}
    />
  </section>

  <section>
    <h2>Volunteer Signup</h2>
    <VolunteerSignup volunteers={volunteers} onAdd={addVolunteer} onRemove={removeVolunteer} />
  </section>

  <section>
    <h2>Pantry Inventory</h2>
    <PantryInventory
      pantry={pantry}
      onAdd={addPantryItem}
      onUpdate={updatePantry}
      onRemove={removePantry}
    />
  </section>
</main>

<style>
  main { padding: 1rem; max-width: 800px; margin: auto; }
  section { margin-bottom: 2rem; }
  h1 { margin-bottom: 1rem; }
</style>
