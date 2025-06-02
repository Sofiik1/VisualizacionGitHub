<script>
  import JavaScript from './JavaScript.svelte';
  import DoubleDiamondIcon from './DoubleDiamondIcon.svelte';
  import CSS from './CSS.svelte';
  import C from './C.svelte';
  import Svelte from './Svelte.svelte';
  import Python from './Py.svelte';
  import SemiArcsIcon from './SemiArcsIcon.svelte';
  import WavyLineIcon from './WavyLineIcon.svelte';
  import WavyLineIcon2 from './WavyLineIcon.svelte';
  import WavyLineIcon3 from './WavyLineIcon.svelte';
  import WavyLineIcon4 from './WavyLineIcon.svelte';
  import StarIcon from './StarIcon.svelte';
  import Html from './Html.svelte';
  import Cmasmas from './Cmasmas.svelte';
  import WavyLineHueco from './WavyLineHueco.svelte';


  let mostrarGrilla = false;
  let mostrarReferencias = false;
  let referenciasActivas = false;
  let grillaActiva = false;

  import Papa from 'papaparse';
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  const iconLayout = {
  JavaScript:        { x: '45%', y: '20%',    scale: 4},
  DoubleDiamondIcon: { x: '15%', y: '50%',   scale: 1.5 },
  CSS:               { x: '33%', y: '75%',   scale: 5.5 },
  C:                 { x: '50%', y: '50%',   scale: 6.5 },
  Svelte:            { x: '80%', y: '70%',   scale: 8.2 },
  Python:            { x: '34%', y: '50%',   scale: 7 },
  SemiArcsIcon:      { x: '90%', y: '85%',   scale: 1.5 },
  Html:              { x: '85%', y: '62%',   scale: 6 },
  Cmasmas:           { x: '43%', y: '40%',   scale: 7 },

  StarIcon:          { x: '85%', y: '14%',   zIndex: 9, scale: 1.5 },
  WavyLineIcon:      { x: '0%',  y: '50%',   zIndex: 20, scale: 6.5 },
  WavyLineHueco:     { x: '0%',  y: '50%',   zIndex: 20, scale: 6.5 },

};


  let Repositorios = [];

  function parseDateDDMMYYYY(fechaStr) {
  const [day, month, year] = fechaStr.split('/').map(Number);
  return new Date(year, month - 1, day); // JavaScript months are 0-indexed
}

function parseColaboradoresFromCSV(csvText) {
  if (csvText.charCodeAt(0) === 0xFEFF) {
    csvText = csvText.slice(1);
  }

  const { data, errors } = Papa.parse(csvText, {
    header: true,
    skipEmptyLines: true,
    dynamicTyping: true,
    delimiter: ","
  });

  if (errors.length) {
    console.error('CSV Parse Errors:', errors);
  }

  const commitsArray = data.map(row => row.commits);
  const minCommits = d3.min(commitsArray);
  const maxCommits = d3.max(commitsArray);

  const starScale = d3.scaleLinear()
    .domain([minCommits, maxCommits])
    .range([0.3, 1.5]);

  const parsedRepos = data.map(row => {
    const fechaParsed = parseDateDDMMYYYY(row.fecha);

    const languages = [
      { name: 'Python', value: row.python },
      { name: 'JavaScript', value: row.javascript },
      { name: 'CSS', value: row.css },
      { name: 'Html', value: row.html },
      { name: 'Svelte', value: row.svelte },
      { name: 'C', value: row.c },
      { name: 'Cmasmas', value: row.cmas },
    ].filter(lang => lang.value > 0);

    languages.sort((a, b) => a.value - b.value);

    const baseIcons = languages.map(lang => lang.name);
    const wavyIconName = row.gusto === 1 ? 'WavyLineIcon' : 'WavyLineHueco';
    const allIcons = ['StarIcon', ...baseIcons, wavyIconName];


    const iconLayoutRow = {};
    allIcons.forEach((iconName, i) => {
      const base = iconLayout[iconName];
      if (base) {
        iconLayoutRow[iconName] = { ...base };
        if (!('zIndex' in base)) {
          iconLayoutRow[iconName].zIndex = i;
        }
      }
    });

    return {
      nombre: row.nombre,
      fecha: fechaParsed,
      commits: row.commits,
      peso: row.peso,
      gusto: row.gusto,
      poco: row.poco,
      starScale: starScale(row.commits),
      iconos: allIcons,
      iconLayout: iconLayoutRow
    };
  });

  // 🔽 Sort by date ascending
  parsedRepos.sort((a, b) => a.fecha - b.fecha);

  return parsedRepos;
}

onMount(async () => {
  try {
    const response = await fetch('/datos.csv');
    let csvText = await response.text();

    if (csvText.charCodeAt(0) === 0xFEFF) {
      csvText = csvText.slice(1);
    }

    Repositorios = parseColaboradoresFromCSV(csvText);
  } catch (e) {
    console.error('Error fetching CSV:', e);
  }
});

  const iconComponents = {
    JavaScript,
    DoubleDiamondIcon,
    CSS,
    C,
    Svelte,
    Python,
    SemiArcsIcon,
    WavyLineIcon,
    StarIcon,
    Html,
    Cmasmas,
    WavyLineHueco
  };

 
 const max_size = 1.6   
 const baseIconSize = 50;  // for example, 50px base size
 const iconLayoutRow = JSON.parse(JSON.stringify(iconLayout));

 function formatDateToDDMMYYYY(date) {
  const day = String(date.getDate()).padStart(2, '0');
  const month = String(date.getMonth() + 1).padStart(2, '0'); // months are 0-indexed
  const year = date.getFullYear();
  return `${day}/${month}/${year}`;
}

  function getIcons(lenguajes) {
    if (!Array.isArray(lenguajes)) return [];
    return lenguajeIcons
      .filter(icon => lenguajes.includes(icon.nombre))
  }

</script>

<main class="page">
  <h1 class="title">Repographix</h1>
  <h2 class="subtitle"> Nuestros repositorios en tarjetas visuales</h2>
<div>
 
<!-- CONTENEDOR CON SCROLL HORIZONTAL -->
<div class="scroll-container">
  {#each Repositorios as t}
    <div class="caja-horizontal">
      <div class="borde-extra" style="border-color: {t.peso == 4 ? '#ffffff' : '#000000'}">
        <div class="borde-extra" style="border-color: {t.peso >= 3 ? '#ffffff' : '#000000'}">
          <div class="borde-extra" style="border-color: {t.peso >= 2 ? '#ffffff' : '#000000'}; padding:5px;">
            <div class="colab-box-BIG-Mora">
              <div class="icon-layer-BIG">
                {#each t.iconos as nombre}
                  {#if iconComponents[nombre] && t.iconLayout[nombre]}
                    <svelte:component
                      this={iconComponents[nombre]}
                      size={baseIconSize * t.iconLayout[nombre].scale * (nombre === 'StarIcon' ? t.starScale : 1)}
                      class="icon-item-BIG"
                      style={`position: absolute;
                              left: ${t.iconLayout[nombre].x};
                              top: ${t.iconLayout[nombre].y};
                              stroke: ${t.iconLayout[nombre].color};
                              transform: translate(-50%, -50%);
                              z-index: ${t.iconLayout[nombre].zIndex ?? 0};
                              pointer-events: none;`}
                    />
                  {/if}
                {/each}
              </div>
              </div>
            </div>
          </div>
        </div>
        <div class="repositorio-info" style="width: 368;">
          <p class="repo-sub-nombre">{t.nombre}</p>
          <p class="repo-sub-fecha">{formatDateToDDMMYYYY(t.fecha)}</p>
        </div>
    </div>
  {/each}
</div>
  
<div class="intro">
  <p class="info">
    Representamos colaboraciones en repositorios de GitHub, correspondientes a trabajos que realizamos a lo largo de nuestra carrera. Para ello, usamos tarjetas visuales
    sintetizando atributos clave como:
    la variedad de lenguajes utilizados, la cantidad de commits, el peso del repositorio y cual fue la satisfacción del usuario con el resultado final de su proyecto.
    Para representar y diferenciar cada una de estas dimensiones, seleccionamos las siguientes formas y colores.
  </p>
</div>

<div>

<button
  class="ref-button {referenciasActivas ? 'activo' : ''}"
  on:click={() => {
    referenciasActivas = !referenciasActivas;
    mostrarReferencias = !mostrarReferencias;
  }}>
  {referenciasActivas ? 'Ocultar referencias' : 'Ver referencias'}
</button>



 {#if mostrarReferencias}
    <div class="legend-wrapper">
      <div class="legend-info">
        <div class="legend-grid-2x2">
          <!-- PESO -->
          <div class="legend-block">
            <!-- Peso content -->
              <h3 class="legend-title">Peso del repositorio</h3>
              <div class="peso-grid">
                <div class="peso-item">
                      <div class="borde-extra-negro">
                        <div class="borde-extra-negro">
                          <div class="borde-extra-negro">
                            <div class="borde-extra">
                              <div class="borde-extra-negro"></div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <span class="ref">1KB - 3KB</span>
                    </div>
                    <div class="peso-item">
                      <div class="borde-extra-negro">
                        <div class="borde-extra-negro">
                          <div class="borde-extra">
                            <div class="borde-extra">
                              <div class="borde-extra-negro"></div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <span class="ref">5KB - 1MB</span>
                    </div>
                    <div class="peso-item">
                      <div class="borde-extra-negro">
                        <div class="borde-extra">
                          <div class="borde-extra">
                            <div class="borde-extra">
                              <div class="borde-extra-negro"></div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <span class="ref">1.1MB - 4MB</span>
                    </div>
                    <div class="peso-item">
                      <div class="borde-extra">
                        <div class="borde-extra">
                          <div class="borde-extra">
                            <div class="borde-extra">
                              <div class="borde-extra-negro"></div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <span class="ref">5MB - 33MB</span>
                    </div>
                  </div>
                </div>
                  

          <!-- SUPERPOSICIÓN -->
          <div class="legend-block">
            <!-- Superposición content -->
              <h3 class="legend-title">Superposición</h3>
              <div class="superposicion-container">
                <div class="colab-box-referencia">
                  <div class="icon-layer-referencia">
                    <!-- Icon 1 -->
                    <svelte:component
                      this={iconComponents['Cmasmas']}
                      size={baseIconSize * iconLayout['Cmasmas'].scale * 0.5}
                      class="icon-item-BIG"
                      style={`position: absolute;
                              left: ${iconLayout['Cmasmas'].x};
                              top: ${iconLayout['Cmasmas'].y};
                              stroke: ${iconLayout['Cmasmas'].color ?? 'black'};
                              transform: translate(-50%, -50%);
                              z-index: ${iconLayout['Cmasmas'].zIndex ?? 0};
                              pointer-events: none;`}
                    />
                    <!-- Icon 2 -->
                    <svelte:component
                      this={iconComponents['Python']}
                      size={baseIconSize * iconLayout['Python'].scale * 0.5}
                      class="icon-item-BIG"
                      style={`position: absolute;
                              left: ${iconLayout['Python'].x};
                              top: ${iconLayout['Python'].y};
                              stroke: ${iconLayout['Python'].color ?? 'black'};
                              transform: translate(-50%, -50%);
                              z-index: ${iconLayout['Python'].zIndex ?? 0};
                              pointer-events: none;`}
                    />
                  </div>
                </div>
                <div class="colab-box-referencia">
                  <div class="icon-layer-referencia">
                    <!-- Icon 1 -->
                    <svelte:component
                      this={iconComponents['Python']}
                      size={baseIconSize * iconLayout['Python'].scale * 0.5}
                      class="icon-item-BIG"
                      style={`position: absolute;
                              left: ${iconLayout['Python'].x};
                              top: ${iconLayout['Python'].y};
                              stroke: ${iconLayout['Python'].color ?? 'black'};
                              transform: translate(-50%, -50%);
                              z-index: ${iconLayout['Python'].zIndex ?? 0};
                              pointer-events: none;`}
                    />
                    <!-- Icon 2 -->
                    <svelte:component
                      this={iconComponents['Cmasmas']}
                      size={baseIconSize * iconLayout['Cmasmas'].scale * 0.5}
                      class="icon-item-BIG"
                      style={`position: absolute;
                              left: ${iconLayout['Cmasmas'].x};
                              top: ${iconLayout['Cmasmas'].y};
                              stroke: ${iconLayout['Cmasmas'].color ?? 'black'};
                              transform: translate(-50%, -50%);
                              z-index: ${iconLayout['Cmasmas'].zIndex ?? 0};
                              pointer-events: none;`}
                    />
                  </div>
                </div>
              </div>
              <p class="superposicion-text">
                Mientras más se usó un lenguaje, más arriba aparece en relación al resto.
              </p>
            </div>

          <!-- SATISFACCIÓN -->
          <div class="legend-block">
             <h3 class="legend-title">Grado de satisfacción</h3>
              <div class="legend-vertical-list">
                <div class="container-wavy"> <WavyLineIcon size={180} /> <p class="ref">Satisfecho</p> </div>
                <div class="container-wavy"> <WavyLineHueco size={180} /> <p class="ref">Insatisfecho</p> </div>
              </div>
            </div>

          <!-- COMMITS -->
          <div class="legend-block">
            <!-- Commits content -->
            <h3 class="legend-title">Cantidad de Commits</h3>
              <div class="container-wavy">
                <div class="legend-icon-horizontal">
                  <div class="legend-icon-stack"> <StarIcon size={25} /></div>
                  <div class="legend-icon-stack"> <StarIcon size={65} /> </div>
                  <div class="legend-icon-stack"> <StarIcon size={130} /> </div>
                </div>
                <div class = "text-com">
                  <p class="ref">Mayor cantidad de commits, más grande la estrella.</p>
                </div>
                </div>
            </div>
            
            <div class="legend-block" style="grid-column: span 2;">
            <h3 class="legend-title" >Lenguajes usados:</h3>
            <div class="legend-icon-grid">
              <div> <Html size={60} /> <p>HTML</p> </div>
              <div> <Python size={60} /> <p>Python</p> </div>
              <div> <JavaScript size={60} /> <p>JavaScript</p> </div>
              <div> <Cmasmas size={60} /> <p>C++</p> </div>
              <div> <C size={60} /> <p>C</p> </div>
              <div> <Svelte size={60}/> <p>Svelte</p> </div>
              <div> <CSS size={60} /> <p>CSS</p> </div>
            </div>
          </div>
          
        </div>
    </div>
  </div>
{/if}

<button
  class="ref-button {grillaActiva ? 'activo' : ''}"
  on:click={() => {
    grillaActiva = !grillaActiva;
    mostrarGrilla = !mostrarGrilla;
  }}>
  {grillaActiva ? 'Ocultar Repos' : 'Ver todos los Repos'}
</button>

{#if mostrarGrilla}  
 <h1 class="title">Grilla de todos los repositorios</h1>
  <div class="cajas">
    {#each Repositorios as t}
      <div class="caja">
        <div class="borde-extra" style= "border-color: {t.peso==4 ? '#ffffff' : '#000000'};">
          <div class="borde-extra" style= "border-color: {t.peso>=3 ?  '#ffffff' : '#000000'};">
            <div class="borde-extra" style= "border-color: {t.peso>=2 ? '#ffffff' : '#000000'}; padding:3.5px;">
              <div class="colab-box-BIG">
                <div class="icon-layer-BIG">

                    {#each t.iconos as nombre}
                      {#if iconComponents[nombre] && t.iconLayout[nombre] }
                        <svelte:component
                          this={iconComponents[nombre]}
                          size={baseIconSize * t.iconLayout[nombre].scale * .9 * (nombre === 'StarIcon' ? t.starScale : 1 )}
                          class="icon-item-BIG"
                          style={`position: absolute;
                                  left: ${t.iconLayout[nombre].x};
                                  top: ${t.iconLayout[nombre].y};
                                  stroke= ${t.iconLayout[nombre].color};
                                  transform: translate(-50%, -50%);
                                  z-index: ${t.iconLayout[nombre].zIndex ?? 0};
                                  pointer-events: none;`}
                        />
                      {/if}
                    {/each}
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="repositorio-info"style="width: 329px;">
          <p class="repo-sub-nombre">{t.nombre}</p>
          <p class="repo-sub-fecha">{formatDateToDDMMYYYY(t.fecha)}</p>
        </div>
      </div>
    {/each}
  </div>
{/if}

  <footer class="footer">
    <div class="footer-content">
      <a href="https://github.com/ezemaut/VisualizacionFinal" target="_blank">Repositorio en GitHub</a>
      <span>|</span>
      <a href="https://www.linkedin.com/in/sofia-kutter" target="_blank">Sofía Kutter</a>
      <span>|</span>
      <a href="https://www.linkedin.com/in/ezequiel-mautner/" target="_blank">Ezequiel Mautner</a>
      <span>|</span>
      <a href="https://www.linkedin.com/in/morafernandezstickar/" target="_blank">Mora Fernandez</a>
    </div>
  </footer>
</main>

<style>

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
  }


</style>