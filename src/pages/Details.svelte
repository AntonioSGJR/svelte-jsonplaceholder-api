<script>
  export let id;
  import { onMount } from 'svelte'  
  import { writable } from 'svelte/store';

  let albumState = writable({});
  let photosState = writable([]);
  let album;

  albumState.subscribe(value => album = value);

  onMount(() => {
    fetch(`https://jsonplaceholder.typicode.com/albums/${id}`)
    .then(response => response.json())
    .then(albums => {
      albumState.set(albums);
    })
    .catch(error => {
      console.log(error);
      return [];
    });

    fetch(`https://jsonplaceholder.typicode.com/albums/${id}/photos`)
    .then(response => response.json())
    .then(photos => {
      photosState.set(photos);
    })
    .catch(error => {
      console.log(error);
      return [];
    });
  });
</script>

<main>
    <h1>{album.title}</h1>
    <p>Album: {album.id}</p>
    <p>Usuario: {album.userId}</p>
    <h2>Photos</h2>
    <div class="photos">
      {#each $photosState as photo}
        <img src="{photo.thumbnailUrl}" alt="Album photo" class="card">
      {/each}
    </div>
</main>

<style>
main {
  padding: 0rem 1rem 1rem 1rem;
}

.photos {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(9rem, 1fr));
  gap: 1rem;
}

</style>