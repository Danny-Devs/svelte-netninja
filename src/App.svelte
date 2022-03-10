<script>
  import Modal from './Modal.svelte';
  import AddPersonForm from './AddPersonForm.svelte';

  let showModal = false;

  let people = [
    {
      name: 'yoshi',
      beltColour: 'black',
      age: 25,
      skills: ['sneaking'],
      id: 1,
    },
    {
      name: 'mario',
      beltColour: 'orange',
      age: 45,
      skills: ['fighting'],
      id: 2,
    },
    {
      name: 'luigi',
      beltColour: 'brown',
      age: 35,
      skills: ['running', 'sneaking'],
      id: 3,
    },
  ];

  const handleClick = (e, id) => {
    people = people.filter((person) => person.id !== id);
  };

  const toggleModal = () => {
    showModal = !showModal;
  };

  const addPerson = (e) => {
    people = [e.detail, ...people];
    showModal = false;
  };
</script>

<Modal isPromo={false} {showModal} on:click={toggleModal}>
  <AddPersonForm on:addPerson={addPerson} {toggleModal} />
</Modal>

<main>
  <button on:click={toggleModal}>Show modal</button>
  {#each people as person (person.id)}
    <div>
      <h4>{person.name}</h4>
      {#if person.beltColour === 'black'}
        <p><strong>master ninja</strong></p>
      {/if}
      <p>
        {person.age} years old, {person.beltColour} belt. Skills: {person.skills}
      </p>
      <button on:click={(e) => handleClick(e, person.id)}>Delete</button>
    </div>
  {:else}
    <p>There are no people to show...</p>
  {/each}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
