<script>
  import Anteojos from './Anteojos.svelte';
  let colores = [
    "#b24fe1", "#009688", "#009b01", "#8bc34a", "#ff8acb", "#f03800", "#c9b8f8"
  ];
  let sombreroHeight = 90;
  
</script>

<div class="card">
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


  <img src="/sombrero.png" alt="Sombrero" class="sombrero" style={`height: ${sombreroHeight}px`} />

  <div class="gato-wrapper">
    <img src="/gitcat.png" alt="Octocat" class="gato" />
  </div>
  <div class="name">
    <p>Sofía Kutter</p>
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
  }

  .arcoiris {
    position: absolute;
    align-items: center;
    top: 15%;
    left: 60%;
    transform: translateX(-50%);
    z-index: 0;
  }

  .gato-wrapper {
    grid-row: 2 / span 2;
    grid-column: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    margin-top: -22%;
  }

  .gato {
    width: 280px;
    max-height: 280px;
    object-fit: contain;
    z-index: 2;
  }

  .sombrero {
    position: absolute;
    top: 12%;
    left: 50%;
    transform: translateX(-50%);
    z-index: 3;
  }

  .name{
    grid-row: 3;
    grid-column: 2;
    display: flex;
    justify-content: center;   /* centrar horizontalmente */
    align-items: end;          /* alinear al fondo */
    height: 95%;
  }
</style>
