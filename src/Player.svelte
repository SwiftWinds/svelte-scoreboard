<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let id;
  export let name;
  export let points;
  let showControls = false;

  const addPoint = () => (points += 1);
  const removePoint = () => (points -= 1);
  const toggleControls = () => (showControls = !showControls);
  const removePlayer = e => {
    e.preventDefault();
    dispatch("removeplayer", id);
  };
</script>

<style>
  h1 {
    color: #204f6e;
  }

  h3 {
    margin-bottom: 10px;
  }

  .player-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>

<div class="card">
  <header class="player-info">
    <h1>
      {name}
      <button class="btn btn-sm" on:click={toggleControls}>
        {#if showControls}-{:else}+{/if}
      </button>
      <button class="btn btn-danger btn-sm" on:click={removePlayer}>-</button>
    </h1>
    <p class="id">ID: {id}</p>
  </header>
  <h3>Points: {points}</h3>
  {#if showControls}
    <button class="btn" on:click={addPoint}>+1</button>
    <button class="btn btn-dark" on:click={removePoint}>-1</button>
    <input type="number" bind:value={points} />
  {/if}
</div>
