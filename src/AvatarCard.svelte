
<script>
  export let nombre;
  export let colores = [];
  export let sombreroHeight = 90;
  import SemiCircleStars from './SemiStart.svelte';
  export let commits;

function calcTop(height) {
  const minTop = 85;   // sombrero más chico (repos = 1~2)
  const maxTop = 25;   // sombrero más grande (repos = 16)
  const minHeight = 50;
  const maxHeight = 130;

  const norm = (height - minHeight) / (maxHeight - minHeight); // [0,1]
  const eased = 1 - Math.pow(1 - norm, 1.8); // curva suavizada
  return minTop - eased * (minTop - maxTop);
}

</script>

<div class="card">
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
    src="/sombrero.png"
    alt="Sombrero"
    class="sombrero"
    style={`height: ${sombreroHeight}px; top: ${calcTop(sombreroHeight)}px;`}
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
</div>

<style>
  .card {
    display: grid;
    grid-template-rows: 1fr 1fr 1fr;
    grid-template-columns: 1fr 1fr 1fr;
    height: 350px;
    width: 300px;
    position: relative;
    border: 2px solid rgba(0, 255, 200, 0.364); 
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
    width: 280px;
    max-height: 280px;
    object-fit: contain;
    z-index: 3;
  }

  .sombrero {
    position: absolute;
    top: 15%;
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
    margin-top: -10%;
    left: 50%;
    transform: translateX(-50%);
    z-index: 10;
  }

  
</style>
