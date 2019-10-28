<script>
  import Navbar from "./Navbar.svelte";
  import Player from "./Player.svelte";
  import AddPlayer from "./AddPlayer.svelte";

  let players = [
    {
      name: "John Doe",
      points: 53
    },
    {
      name: "Sam Smith",
      points: 45
    },
    {
      name: "Sara Wilson",
      points: 34
    }
  ];

  const addPlayer = e => {
    const newPlayer = e.detail;
    players = [...players, newPlayer];
  };

  const removePlayer = e => {
    const removedId = e.detail;
    players.splice(removedId, 1);
    players = players;
  };
</script>

<Navbar />
<div class="container">
  <AddPlayer on:addplayer={addPlayer} />
  {#if players.length === 0}
    <p>No Players</p>
  {:else}
    {#each players as player, i}
      <Player
        name={player.name}
        points={player.points}
        id={i}
        on:removeplayer={removePlayer} />
    {/each}
  {/if}
</div>
