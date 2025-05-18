<!-- BrushZIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#b24fe1"; // violeta intenso
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
    d="M0 50 
    L40 20 
    L25 55 
    L55 30 
    L50 60 
    L70 40"
    stroke={color}
    stroke-width="6"
    stroke-linecap="round"
    stroke-linejoin="round"
    fill="none"
  />
</svg>