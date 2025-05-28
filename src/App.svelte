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



  import Papa from 'papaparse';
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  const iconLayout = {
  JavaScript:        { x: '45%', y: '20%',    scale: 4, color: '#0'},
  DoubleDiamondIcon: { x: '15%', y: '50%',   scale: 1.5 },
  CSS:               { x: '33%', y: '75%',   scale: 5 },
  C:                 { x: '50%', y: '50%',   scale: 6.5 },
  Svelte:            { x: '80%', y: '95%',   scale: 8.2 },
  Python:            { x: '34%', y: '50%',   scale: 7 },
  SemiArcsIcon:      { x: '90%', y: '85%',   scale: 1.5 },
  Html:              { x: '85%', y: '62%',   scale: 6 },
  Cmasmas:           { x: '40%', y: '40%',   scale: 7 },

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
    .range([0.5, 1.5]);

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


//  CODIGO MORA
   const lenguajeIcons = [
    { nombre: 'javascript', componente: JavaScript },
    { nombre: 'c++', componente: Cmasmas },
    { nombre: 'css', componente: CSS },
    { nombre: 'c', componente: C },
    { nombre: 'svelte', componente: Svelte },
    { nombre: 'python', componente: Python },
    { nombre: 'html', componente: Html }

  ];

  function getIcons(lenguajes) {
    if (!Array.isArray(lenguajes)) return [];
    return lenguajeIcons
      .filter(icon => lenguajes.includes(icon.nombre))
  }

  let boxScale = 0.8; // or any value like 0.8, 1.5, etc.



</script>

<main class="page">
  <h1 class="title">Repographix</h1>
<h2 class="subtitle"> Nuestros repositorios en tarjetas visuales</h2>
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
      <div class="repositorio-info">
      <p class="repo-sub-nombre">{t.nombre}</p>
      <p class="repo-sub-fecha">{formatDateToDDMMYYYY(t.fecha)}</p>
      </div>
    </div>
  {/each}
</div>

<div class="intro">
 <h1 class="title">Repositorios GitHub</h1>
  <p class="info">
    Representamos colaboraciones en repositorios de GitHub, correspondientes a trabajos que realizamos a lo largo de nuestra carrera. Para ello, usamos tarjetas visuales
    sintetizando atributos clave como:
    la variedad de lenguajes utilizados, la cantidad de commits, el peso del repositorio y cual fue la satisfacción del usuario con el resultado final de su proyecto.
    Para representar y diferenciar cada una de estas dimensiones, seleccionamos las siguientes formas y colores.
  </p>
</div>
  <div class="legend-wrapper">
      <div class="legend-grid">
          <div class="legend-block">
              <h3 class="legend-title">Peso del repositorio</h3>
              <div class="legend-row peso-grid">
                <div class="legend-item">
                  <div class="borde-extra-negro">
                    <div class="borde-extra-negro">
                      <div class="borde-extra-negro">
                        <div class="borde-extra"><div class="borde-extra-negro"></div></div>
                      </div>
                    </div>
                  </div>
                   <span class="ref">0 - 20KB</span>
                </div>
                <div class="legend-item">
                  <div class="borde-extra-negro">
                    <div class="borde-extra-negro">
                      <div class="borde-extra">
                        <div class="borde-extra"><div class="borde-extra-negro"></div></div>
                      </div>
                    </div>
                  </div>
                  <span class="ref">20KB - 60KB</span>
                </div>
                <div class="legend-item">
                  <div class="borde-extra-negro">
                    <div class="borde-extra">
                      <div class="borde-extra">
                        <div class="borde-extra"><div class="borde-extra-negro"></div></div>
                      </div>
                    </div>
                  </div>
                  <span class="ref">60KB - 3GB</span>
                </div>
                <div class="legend-item">
                  <div class="borde-extra">
                    <div class="borde-extra">
                      <div class="borde-extra">
                        <div class="borde-extra"><div class="borde-extra-negro"></div></div>
                      </div>
                    </div>
                  </div>
                  <span class="ref">4GB - 10GB</span>
                </div>
              </div>
            </div>

          <div class="legend-block">
            <h3 class="legend-title">Grado de satisfacción</h3>
            <div class="legend-vertical-list">
              <div class="legend-icon-horizontal">
                <WavyLineIcon size={120} />
                <p class="ref">Satisfecho</p>
              </div>
              <div class="legend-icon-horizontal">
                <WavyLineHueco height={100} size={120} />
                <p class="ref">Insatisfecho</p>
              </div>
            </div>
          </div>

          <div class="legend-block">
            <h3 class="legend-title">Commits</h3>
            <div class="legend-icon-horizontal">
              <div class="legend-icon-stack">
                <StarIcon size={30} />
                <StarIcon size={50} />
                <StarIcon size={70} />
                <StarIcon size={80} />
              </div>
              <p class="commit-description">
                El tamaño varia según la cantidad de commits realizados.
              </p>
            </div>
          </div>
          
      </div>
      <div class="legend-block">
      <h3 class="legend-title">Lenguajes usados: </h3>
      <div class="legend-icon-grid">
          <div ><Html size={60}  /> 
            <p>HTML</p>
          </div>
          <div><Python size={60}  /> 
            <p>Python</p>
          </div>
          <div><JavaScript size={60} /> 
            <p>JavaScript</p>
          </div>
          <div><Cmasmas size={60}/> 
            <p>C++</p>
          </div>
          <div><C size={60}/> 
            <p>C</p>
          </div>
          <div><Svelte size={70} /> 
            <p>Svelte</p>
          </div>
          <div><CSS size={60}/> 
            <p>CSS</p>
          </div>
      </div>
      </div>
  </div>
 <h1 class="title">Bordes distintos</h1>
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
        <div class="repositorio-info">
          <p class="repo-sub-nombre">{t.nombre}</p>
          <p class="repo-sub-fecha">{formatDateToDDMMYYYY(t.fecha)}</p>
        </div>
      </div>
    {/each}
  </div>


  <footer class="footer">
    <div class="footer-content">
      <a href="https://github.com/ezemaut/VisualizacionFinal" target="_blank">Repositorio en GitHub</a>
      <span>|</span>
      <a href="https://www.linkedin.com/in/sofia-kutter" target="_blank">Sofía Kutter</a>
      <span>|</span>
      <a href="https://www.linkedin.com/in/ezequiel-mautner/" target="_blank">Ezequiel Mautner</a>
      <span>|</span>
      <a href="https://www.linkedin.com/in/ezequiel-mautner/" target="_blank">Mora Fernandez</a>
    </div>
  </footer>
</main>

<style>

  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
  }


</style>
