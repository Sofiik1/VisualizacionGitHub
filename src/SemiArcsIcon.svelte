<!-- SemiArcsIcon.svelte -->
<script>
    export let size = 64;
    export let color1 = "#a0d911"; // verde lima
    export let color2 = "#2c2f34"; // gris oscuro
    export let style = "";
    </script>
  
  <svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 100 100"
  width={size}
  height={size}
  fill="none"
  style={style}
  >
    <!-- Verde (derecha) -->
    <path d="M50 50 A20 20 0 0 1 70 70" stroke={color1} stroke-width="8" fill="none" />
    <path d="M50 50 A30 30 0 0 1 80 80" stroke={color1} stroke-width="8" fill="none" />
    <path d="M50 50 A40 40 0 0 1 90 90" stroke={color1} stroke-width="8" fill="none" />
  
    <!-- Negro (izquierda), simétricos -->
    <path d="M50 50 A20 20 0 0 0 30 70" stroke={color2} stroke-width="8" fill="none" />
    <path d="M50 50 A30 30 0 0 0 20 80" stroke={color2} stroke-width="8" fill="none" />
    <path d="M50 50 A40 40 0 0 0 10 90" stroke={color2} stroke-width="8" fill="none" />
  </svg>