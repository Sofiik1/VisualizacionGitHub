
<script>
  export let nombre;
  export let colores = [];
  export let sombreroHeight = 90;
  import SemiCircleStars from './SemiStart.svelte';
  export let commits;
  export let modoPopup = false;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  function handleClick() {if (modoPopup) return;
    dispatch('select', { nombre, colores, sombreroHeight, commits});
  }

import { scaleLinear } from 'd3-scale';
    import Cordon from './Cordon.svelte';

const calcHeight = scaleLinear()
  .domain([1, 15])     // number of repos (or whatever metric)
  .range([0, 7])    // height in pixels

</script>
<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
  class={`cursor-pointer ${modoPopup ? 'popup-avatar' : 'scrolling-avatar'}`}
  on:click={handleClick}
>


<div class="card" >
  <!-- Arcoíris de lenguajes -->
  <div class="arcoiris">
    <svg width="360" height="450" viewBox="0 0 360 450">
      {#each colores as color, i}
        <path
          d={`M${40 + i * 11},250 A${50 - i * 3},110 0 0 1 ${250 - i * 11},250`}
          stroke={color}
          stroke-width="5"
          fill="none"
        />
      {/each}
    </svg>
  </div>

  <img
  src="/chapa.png"
  alt="chapa"
  class="chapa"
  style={`height: ${calcHeight(sombreroHeight)}px;`}
 />


  <div class="gato-wrapper">
    <img src="/gitcat.png" alt="Octocat" class="gato" />
  </div>

  <div class="name">
    <p>{nombre}</p>
  </div>

  <div class="SemiStar">
  <SemiCircleStars commits={commits} maxCommits={200} />
</div>
<div class="Cordon">
  <Cordon/>
</div>
</div>
</div>

<style>
  .card {
    display: grid;
    grid-template-rows: 1fr 1fr 1fr;
    grid-template-columns: 1fr 1fr 1fr;
    height: 350px;
    width: 300px;
    position: relative;
    border: 2px solid rgba(236, 249, 246, 0.767); 
    border-radius: 16px;
    background: black;
    box-shadow:
      0 0 12px rgba(0, 255, 200, 0.15),
      0 0 24px rgba(0, 255, 200, 0.15) inset;
    backdrop-filter: blur(6px);
    transition: box-shadow 0.3s ease;
    margin: 1rem;
  }

  .arcoiris {
    position: absolute;
    align-items: center;
    top: 15%;
    left: 60%;
    transform: translateX(-50%);
    z-index: 1;
  }

  .gato-wrapper {
    grid-row: 2 / span 2;
    grid-column: 2; 
    
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 2;
    margin-top: -22%;
  }

  .gato {
    width: 250px;
    max-height: 280px;
    object-fit: contain;
    z-index: 3;
  }

  .chapa {
    position: absolute;
    top: 66%;
    left: 50%;
    transform: translateX(-50%);
    z-index: 40000;
  }

  .Cordon {
    position: absolute;
    top: 65%;
    left: 50%;
    transform: translateX(-50%);
    z-index: 4;
  }

  .name {
    grid-row: 3;
    grid-column: 2;
    display: flex;
    justify-content: center;
    align-items: end;
    height: 95%;
    color: white;
  }

  .SemiStar {
    position: absolute;
    margin-top: -5%;
    left: 50%;
    transform: translateX(-50%);
    z-index: 10;
  }

  /* Estilos para modo modal */
.popup-avatar .card {
  margin: 0 auto; /* centrar la card en el modal */
  border: 2px solid rgba(236, 249, 246, 0.767); 
  height: 400px;
}

.popup-avatar .gato-wrapper {
  margin-top: -18%; /* menos empuje hacia arriba */
}

.popup-avatar .gato {
  position: absolute;
  top: 20%;
}

.popup-avatar .name{
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;

}

.popup-avatar .name p {
  white-space: nowrap;
  overflow: hidden;
}

.popup-avatar .chapa {
  max-height: 40px;
  top: 62%;
}

.popup-avatar .Cordon {
  max-height: 35px;
  top: 58%;
}
.popup-avatar .chapa {
  max-height: 40px;
  top: 58%;
}

.popup-avatar .SemiStar {
  margin-top: -5%;
}

.popup-avatar .arcoiris {
  top: 13%;
  left: 60%;
  transform: translateX(-50%);
}
  
</style>
