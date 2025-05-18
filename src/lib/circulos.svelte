
<script>

    import * as d3 from "d3";
    
    let numbers = [24, 33, 42, 54, 63, 71, 77, 87, 92, 98];
    
    // 🔹 Generar todas las posiciones permitidas (evitando fila 1 y columnas 1 y 6)
    let allPositions = [];
    for (let col = 2; col <= 5; col++) {
      for (let row = 2; row <= 5; row++) {
        allPositions.push({ col, row });
      }
    }
    
    // 🔹 Clasificar posiciones en "best", "worst" y "normal"
    let best = [ { col: 2, row: 2 }, { col: 2, row: 5 }, { col: 5, row: 2 }, { col: 5, row: 5 } ];
    let worst = [ { col: 3, row: 3 }, { col: 3, row: 4 }, { col: 4, row: 3 }, { col: 4, row: 4 } ];
    
    // 🔹 Las normales son todas las demás que no estén en "best" ni "worst"
    let normal = allPositions.filter(pos =>
      !best.some(b => b.col === pos.col && b.row === pos.row) &&
      !worst.some(w => w.col === pos.col && w.row === pos.row)
    );
    let positions = [];
    
    for (let n of numbers) {
      let pos;
      if (n >= 87 && best.length > 0) {
        let index = Math.floor(Math.random() * best.length);
        pos = best.splice(index, 1)[0]; // Elimina y asigna la posición
      } else if (n <= 42 && worst.length > 0) {
        let index = Math.floor(Math.random() * worst.length);
        pos = worst.splice(index, 1)[0];
      } else if (normal.length > 0) {
        let index = Math.floor(Math.random() * normal.length);
        pos = normal.splice(index, 1)[0];
      } else {
        // Si todas las listas están vacías, asigna una posición aleatoria
        pos = { col: Math.floor(Math.random() * 5) + 1, row: Math.floor(Math.random() * 5) + 1 };
      }
    
      positions.push({ value: n, col: pos.col, row: pos.row });
    }
    
    console.log(positions);
    
    </script> 
<!-- <script>
    <script>
        import * as d3 from "d3";
      
        export let numbers = [24, 33, 42, 54, 63, 71, 77, 87, 92, 98];
      
        export function generatePositions(numbers) {
          let allPositions = [];
          for (let col = 2; col <= 5; col++) {
            for (let row = 2; row <= 5; row++) {
              allPositions.push({ col, row });
            }
          }
      
          let best = [ { col: 2, row: 2 }, { col: 2, row: 5 }, { col: 5, row: 2 }, { col: 5, row: 5 } ];
          let worst = [ { col: 3, row: 3 }, { col: 3, row: 4 }, { col: 4, row: 3 }, { col: 4, row: 4 } ];
          let normal = allPositions.filter(pos =>
            !best.some(b => b.col === pos.col && b.row === pos.row) &&
            !worst.some(w => w.col === pos.col && w.row === pos.row)
          );
      
          let positions = [];
          for (let n of numbers) {
            let pos;
            if (n >= 87 && best.length > 0) {
              let index = Math.floor(Math.random() * best.length);
              pos = best.splice(index, 1)[0];
            } else if (n <= 42 && worst.length > 0) {
              let index = Math.floor(Math.random() * worst.length);
              pos = worst.splice(index, 1)[0];
            } else if (normal.length > 0) {
              let index = Math.floor(Math.random() * normal.length);
              pos = normal.splice(index, 1)[0];
            } else {
              pos = { col: Math.floor(Math.random() * 5) + 1, row: Math.floor(Math.random() * 5) + 1 };
            }
      
            positions.push({ value: n, col: pos.col, row: pos.row });
          }
      
          console.log("Se generaron posiciones:", positions);
          return positions;
        }
      
        export let positions = generatePositions(numbers);
        
      </script>
      
      <div class="cardinal-container">
        {#each positions as { col, row, value }}
          <div 
            class="circle {value >= 87 ? 'best' : value <= 42 ? 'worst' : 'normal'}"
            style="grid-column-start: {col}; grid-row-start: {row};"
          >
            {value}
          </div>
        {/each}
      </div>
      
      <style>
        .cardinal-container {
          position: relative; 
          width: 100%;
          height: 100%;
          display: grid;
          grid-template-columns: repeat(6, 1fr);
          grid-template-rows: repeat(6, 1fr);
        }
      
        .circle {
          width: 40px;
          height: 40px;
          clip-path: circle(50%);
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 20px;
          color: whitesmoke;
          font-weight: bold;
        }
      
        .best { background-color: green; }  
        .worst { background-color: red; }  
        .normal { background-color: orange; }
      </style> -->
