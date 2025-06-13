<script>
  let lenguajes = [
    { color: "#009b01", nombre: "C" },
    { color:  "#8bc34a", nombre: "C++" },
    { color:  "#ff8acb", nombre: "CSS" },
    { color: "#c9b8f8", nombre: "JavaScript" },
    { color: "#f03800", nombre: "HTML" },
    { color: "#009688", nombre: "Python" },
  ];
</script>

<div class="referencias">
  <h2>Referencias Visuales</h2>

  <div class="bloque">
    <h3>Lenguajes usados</h3>
    <svg width="360" height="450" viewBox="0 0 360 450">
      {#each lenguajes as lang, i}
        <path
            d={`M${40 + i * 11},250 A${50 - i * 3},110 0 0 1 ${250 - i * 11},250`}
            stroke={lang.color}
            stroke-width="5"
            fill="none"
        />
        {/each}

    </svg>

    <div class="lenguaje-claves">
      {#each lenguajes as lang}
        <div class="lenguaje">
          <span class="punto" style={`background-color: ${lang.color}`}></span>
          <span>{lang.nombre}</span>
        </div>
      {/each}
    </div>
  </div>

  <div class="bloque">
    <h3>Tamaño del sombrero según commits</h3>
    <div class="sombreros">
      <div class="caso">
        <img src="/sombrero.png" alt="Sombrero pequeño" style="height: 30px" />
        <p>&lt; 20 commits</p>
      </div>
      <div class="caso">
        <img src="/sombrero.png" alt="Sombrero mediano" style="height: 60px" />
        <p>20–100 commits</p>
      </div>
      <div class="caso">
        <img src="/sombrero.png" alt="Sombrero grande" style="height: 90px" />
        <p>&gt; 100 commits</p>
      </div>
    </div>
  </div>
</div>

<style>
  .referencias {
    color: white;
    padding: 2rem;
    max-width: 500px;
    margin: auto;
  }
  .bloque {
    margin-bottom: 2rem;
  }
  .lenguaje-claves {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem 1rem;
    margin-top: 1rem;
  }
  .lenguaje {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .punto {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    display: inline-block;
  }
  .sombreros {
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin-top: 1rem;
  }
  .caso {
    text-align: center;
  }
  h2, h3 {
    color: #fe1492;
  }
</style>
