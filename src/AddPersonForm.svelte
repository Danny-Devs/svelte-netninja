<script>
  import { createEventDispatcher } from 'svelte';

  let dispatch = createEventDispatcher();
  let name;
  let beltColour;
  let skills = [];

  const addNewPerson = (e) => {
    const newPerson = {
      name,
      beltColour,
      age: +e.target.age.value,
      skills,
      id: Math.random(),
    };
    dispatch('addPerson', newPerson);
  };
</script>

<form on:submit|preventDefault={addNewPerson}>
  <input type="text" name="name" placeholder="name" bind:value={name} />
  <input type="number" name="age" placeholder="age" />
  <label
    >Skills:
    <input type="checkbox" bind:group={skills} value="fighting" />fighting<br />
    <input type="checkbox" bind:group={skills} value="sneaking" />sneaking<br />
    <input type="checkbox" bind:group={skills} value="running" />running<br />
  </label>
  <label
    >Belt colour:
    <select bind:value={beltColour}>
      <option value="black">black</option>
      <option value="red">red</option>
      <option value="orange">orange</option>
      <option value="white">white</option>
    </select>
  </label>
  <button type="submit">Add Person</button>
</form>

<style></style>
