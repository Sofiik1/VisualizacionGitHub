<!-- CurvedRibbonIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#009b01"; // amarillo pastel
  export let style = "";
</script>

<svg
xmlns="http://www.w3.org/2000/svg"
viewBox="0 0 200 200"
width={size}
height={size}
fill="none"
style={style}
>
  <path
    d="M 250 70
   C 50 200, 50 220, 80 -200
   C -20 40, 60 30, 80 -200
"
    stroke={color}
    stroke-width="23"
    stroke-linecap="round"
    stroke-linejoin="round"
    fill="none"
  />
</svg>

  