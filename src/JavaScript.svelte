<!-- SpiralIcon.svelte -->
<script>
  export let color = "#c9b8f8"; // Color violeta pastel
  export let size = 64;         // Tamaño en px
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
  <path
    d="M70 20
  L5 30
  L85 80
  L5 90
  L70 20
"
    stroke={color}
    stroke-width="8"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>
