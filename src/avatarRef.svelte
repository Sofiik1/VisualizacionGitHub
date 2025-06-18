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

<div class="legend-wrapper">
  <h3 class="legend-wrapper-title">Referencias de colaboradores</h3>
  <div class="referencias">
    <div class="bloque">
        <h3 class="legend-title">Lenguajes usados</h3>
        <div class="lenguajes-cont">
          <svg min-width="210" width="210" height="210" viewBox="0 0 260 260">
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
    </div>

    <div class="bloque">
      <h3 class="legend-title">Tamaño del sombrero según commits</h3>
      <div class="sombreros">
        <div class="caso">
          <img src="/sombrero.png" alt="Sombrero pequeño" style="height: 30px" />
          <p>&lt; 20 commits</p>
        </div>
        <div class="caso">
          <img src="/sombrero.png" alt="Sombrero mediano" style="height: 60px" />
          <p>[20, 100] commits</p>
        </div>
        <div class="caso">
          <img src="/sombrero.png" alt="Sombrero grande" style="height: 90px" />
          <p>&gt; 100 commits</p>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .legend-wrapper-title {
    font-size: 2rem;
    font-weight: bold;
    text-align: left;
    margin: 0;
    margin-bottom: 2rem;
    max-width: 100%;
    color: #fe1492;
  }
  .legend-title {
    font-size: 2rem;
    font-weight: normal;
    text-align: left;
    margin: 0;
    margin-bottom: 2rem;
    max-width: 100%;
  }
  .referencias {
    color: white;
    display: flex;
    justify-content: space-between;
  }
  .bloque {
    width: 47%;
  }

  .lenguajes-cont{
    display: flex;
    gap: 5rem;
  }
  .lenguaje {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .lenguaje-claves {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    align-content: center;
    width: 40%;
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
    justify-items: center;
  }
</style>
