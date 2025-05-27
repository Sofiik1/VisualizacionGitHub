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



  import Papa from 'papaparse';
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  const iconLayout = {
  JavaScript:        { x: '45%', y: '20%',    scale: 4, color: '#0'},
  DoubleDiamondIcon: { x: '15%', y: '50%',   scale: 1.5 },
  CSS:               { x: '33%', y: '75%',   scale: 5 },
  C:                 { x: '50%', y: '50%',   scale: 6 },
  Svelte:            { x: '80%', y: '95%',   scale: 8.2 },
  Python:            { x: '34%', y: '50%',   scale: 7 },
  SemiArcsIcon:      { x: '90%', y: '85%',   scale: 1.5 },
  Html:              { x: '85%', y: '62%',   scale: 6 },
  Cmasmas:           { x: '40%', y: '40%',   scale: 7 },

  StarIcon:          { x: '85%', y: '14%',   zIndex: 9, scale: 1.5 },
  WavyLineIcon:      { x: '0%',  y: '50%',   zIndex: 20, scale: 6 },
  WavyLineIcon2:     { x: '5%',  y: '50%',   zIndex: 20, scale: 6 },
  WavyLineIcon3:     { x: '10%', y: '50%',   zIndex: 20, scale: 6 },
  WavyLineIcon4:     { x: '15%', y: '50%',   zIndex: 20, scale: 6 },
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
    const wavyIcons = ['WavyLineIcon', 'WavyLineIcon2', 'WavyLineIcon3', 'WavyLineIcon4'];
    const wavySubset = wavyIcons.slice(0, Math.min(4, row.peso));
    const allIcons = ['StarIcon', ...baseIcons, ...wavySubset];

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
    WavyLineIcon2,
    WavyLineIcon3,
    WavyLineIcon4,
    StarIcon,
    Html,
    Cmasmas
  };

/*  
Combinaciones:
JavaScript, CSS, svelte   -> 'CSS', 'JavaScript', 'Svelte'
Html  -> 'Cmasmas'
python, CSS, Html  -> 'Python', 'JavaScript', 'Cmasmas'
python, Html  -> 'Python', 'Cmasmas'
python  -> 'Python',
python, c++  -> 'Python', 'Html'
python, c  -> 'Python', 'C'
c  -> 'C'

'JavaScript',   JavaScript    
'DoubleDiamondIcon', 
'CSS',         CSS 
'C',              
'Svelte',        Svelte
'Python',          
'SemiArcsIcon',        
'Html',   Html
'Cmasmas'   c++

'WavyLineIcon',   peso   
'StarIcon',       commit   
*/

 

let todos = [
   {  nombre: 'Spotify Skip',
      gusto: true,
      starScale: 1,
      iconos: ['StarIcon','JavaScript', 'CSS', 'Svelte',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: 1,
      iconos: ['StarIcon','Html',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },
   {  nombre: '',
      gusto: true,
      starScale: 1,
      iconos: ['StarIcon','Python', 'CSS', 'Html',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: 1,
      iconos: ['StarIcon','Python', 'Html',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },
   {  nombre: '',
      gusto: true,
      starScale: 1,
      iconos: ['StarIcon','Python',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: 1,
      iconos: ['StarIcon','Python', 'Cmasmas',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },
   {  nombre: '',
      gusto: true,
      starScale: 1,
      iconos: ['StarIcon','Python', 'C',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: 1,
      iconos: ['StarIcon','C',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

]
let todos2 = [
   {  nombre: 'Spotify Skip',
      gusto: true,
      starScale: max_size,
      iconos: ['StarIcon','JavaScript', 'CSS', 'Svelte',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: max_size,
      iconos: ['StarIcon','Html',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },
   {  nombre: '',
      gusto: true,
      starScale: max_size,
      iconos: ['StarIcon','Python', 'CSS', 'Html',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: max_size,
      iconos: ['StarIcon','Python', 'Html',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },
   {  nombre: '',
      gusto: true,
      starScale: max_size,
      iconos: ['StarIcon','Python',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: max_size,
      iconos: ['StarIcon','Python', 'Cmasmas',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },
   {  nombre: '',
      gusto: true,
      starScale: max_size,
      iconos: ['StarIcon','Python', 'C',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

   {  nombre: '',
      gusto: false,
      starScale: max_size,
      iconos: ['StarIcon','C',
        'WavyLineIcon', 'WavyLineIcon2','WavyLineIcon3','WavyLineIcon4',
      ]
    },

]


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



   
</script>

<main class="page">

  <h2 class="subtitulo">Leyenda de íconos</h2>
  <p class="leyenda-subtitulo">Metricas: </p>
  <div class="leyenda">
      <div>
        <div class="borde-extra" style= "border-color:'#4B86AA';">
          <div class="borde-extra" style= "border-color:'#669BBC';">
            <div class="borde-extra" style= "border-color:'#8EB5CD';">
              <div class="borde-extra borde-leyenda" style= "border-color: '#AAC7DA';">
              </div>
            </div>
          </div>
        </div> <span>Peso</span>
      </div>
      <div><WavyLineIcon height={100}, size={100}   /> <span>Cantidad de líneas segun intervalo de peso </span></div>
      <div><StarIcon size={80}  /> <span>Commits, tamaño según cantidad </span></div>
      
  </div>
  <p class="leyenda-subtitulo">Lenguajes usados: </p>
  <div class="leyenda">
      <div ><Html size={80}  /> <span>HTML</span></div>
      <div><Python size={80}  /> <span>Python</span></div>
      <div><JavaScript size={80} /> <span>JavaScript</span></div>
      <div><Cmasmas size={80}  /> <span>C++</span></div>
      <div><C size={80}  /> <span>C</span></div>
      <div><Svelte size={80} /> <span>Svelte</span></div>
      <div><CSS size={80}  /> <span>CSS</span></div>
  </div>




  <h1 class="title">Todos Repos Posibles</h1>
  <div class="cajas">
    {#each todos as t}
      <div class="colab-box-BIG" style="border-color: {t.gusto ? 'limegreen' : 'deeppink'}">
        <div class="icon-layer-BIG">
          {#each t.iconos as nombre}
            {#if iconComponents[nombre] && iconLayout[nombre]}
              <svelte:component
                this={iconComponents[nombre]}
                size={baseIconSize * iconLayout[nombre].scale * (nombre === 'StarIcon' ? t.starScale : 1)}
                class="icon-item-BIG"
                style={`position: absolute;
                        left: ${iconLayout[nombre].x};
                        top: ${iconLayout[nombre].y};
                        transform: translate(-50%, -50%);
                        z-index: ${iconLayout[nombre].zIndex ?? 0};
                        pointer-events: none;`}
              />
            {/if}
          {/each}
        </div>
      </div>
      {/each}
    </div>

    <h1 class="title">Repos de verdad</h1>
    <div class="cajas">
      {#each Repositorios as t}
        <div class="colab-box-BIG" style="border-color: {t.gusto ? 'limegreen' : 'deeppink'}">
          <div class="icon-layer-BIG" >
            {#each t.iconos as nombre}
              {#if iconComponents[nombre] && iconLayout[nombre]}
                <svelte:component
                  this={iconComponents[nombre]}
                  size={baseIconSize * t.iconLayout[nombre].scale * (nombre === 'StarIcon' ? t.starScale : 1)}
                  class="icon-item-BIG"
                  style={`position: absolute;
                          left: ${iconLayout[nombre].x};
                          top: ${iconLayout[nombre].y};
                          transform: translate(-50%, -50%);
                          z-index: ${t.iconLayout[nombre].zIndex ?? 0};
                          pointer-events: none;`}
                />
              {/if}
            {/each}
          </div>
        </div>
      {/each}
    </div>


  <h1 class="title">Bordes distintos</h1>
  <div class="cajas">
    {#each Repositorios as t}
      <div class="caja">
        <div class="borde-extra" style= "border-color: {t.peso==4 ? '#4B86AA' : '#111'};">
        <div class="borde-extra" style= "border-color: {t.peso>=3 ? '#669BBC' : '#111'};">
        <div class="borde-extra" style= "border-color: {t.peso>=2 ? '#8EB5CD' : '#111'}; padding:5px;">
          <div class="colab-box-BIG-Mora">
            <div class="icon-layer-BIG">

                {#each t.iconos as nombre}
                  {#if iconComponents[nombre] && t.iconLayout[nombre] && !/^WavyLineIcon\d*$/.test(nombre)}
                    <svelte:component
                      this={iconComponents[nombre]}
                      size={baseIconSize * t.iconLayout[nombre].scale * (nombre === 'StarIcon' ? t.starScale : 1)}
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
          <p class="repo-sub-nombre">{t.nombre}</p>
          <p class="repo-sub-fecha">{formatDateToDDMMYYYY(t.fecha)}</p>
      </div>
    {/each}
  </div>
          
  


  <h2 class="subtitulo">Leyenda de íconos</h2>
  <div class="leyenda">
    <div>
      <div class="borde-extra" style= "border-color:'#4B86AA';">
        <div class="borde-extra" style= "border-color:'#669BBC';">
          <div class="borde-extra" style= "border-color:'#8EB5CD';">
            <div class="borde-extra borde-leyenda" style= "border-color: '#AAC7DA';">
            </div>
          </div>
        </div>
      </div> <span>Peso</span>
    </div>
    <div><WavyLineIcon height={100}, size={100}   /> <span>Cantidad de líneas segun intervalo de peso </span></div>
    <div><StarIcon size={80}  /> <span>Commits, tamaño según cantidad </span></div>
    <div><Html size={80}  /> <span>HTML</span></div>
    <div><Python size={80}  /> <span>Python</span></div>
    <div><JavaScript size={80} /> <span>JavaScript</span></div>
    <div><Cmasmas size={80}  /> <span>C++</span></div>
    <div><C size={80}  /> <span>C</span></div>
    <div><Svelte size={80} /> <span>Svelte</span></div>
    <div><CSS size={80}  /> <span>CSS</span></div>
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
