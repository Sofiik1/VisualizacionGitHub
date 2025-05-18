<!-- ZigzagIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#f8b400"; // naranja vibrante
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
    d="M30 20 
    L60 30 
    L30 60 
    L80 90"
    stroke={color}
    stroke-width="12"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>