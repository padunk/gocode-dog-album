<script>
  import Loading from './Loading.svelte' // relative path

  export let title;

  let jenisAnjing = []
  let image = [];
  let breed;
  let loading = false;
  let picQty = 1;

  function getJenisAnjing() {
    fetch('https://dog.ceo/api/breeds/list/all')
    .then(response => response.json())
    .then(data => {
      jenisAnjing = Object.keys(data.message)
    })
    .catch(error => console.log(error))
  }

  getJenisAnjing()

  function handleClick() {
    loading = true;

    fetch('https://dog.ceo/api/breed/' + breed + '/images/random/' + picQty)
    .then(response => response.json())
    .then(data => {
      image = data.message
      loading = false
    })
    .catch(error => console.log(error))
  }

</script>

<h1>{title}</h1>

<select bind:value={breed}>
  {#each jenisAnjing as jenis}
  <option value={jenis}>{jenis}</option>
  {/each}
</select>

<input
  type="number"
  name="number"
  min="1"
  max="12"
  step='1'
  bind:value={picQty}
>

<button on:click={handleClick} disabled={loading}>Search
</button>

<div class='photos'>

  {#if loading}
    <Loading text='Loading Album' />
  {:else}
    <div class='outer-wrapper'>
      {#each image as i}
      <div class="img-wrapper">
        <img src="{i}" alt='dogs'>
      </div>
      {/each}
    </div>
  {/if}

</div>

<style>
  h1 {
    color: orangered;
    font-weight: 100;
    text-transform: uppercase;
    font-size: 48px;
  }

  button {
    background: dodgerblue;
    color: white;
    padding: 9px 29px;
  }

  button:disabled {
    background-color: gray;
  }

  img {
    width: 100%;
  }

  .outer-wrapper {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    flex-wrap: wrap;
    row-gap: 20px;
  }

  .img-wrapper {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 200px;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  @media only screen and (min-width: 2560px) {
    h1 {
      font-size: 60px;
      background-color: blue;
    }
  }
</style>