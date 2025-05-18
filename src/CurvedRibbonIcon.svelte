<!-- CurvedRibbonIcon.svelte -->
<!-- CurvedRibbonIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#f8d471"; // amarillo pastel
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 200 200"
  width={size}
  height={size}
  fill="none"
>
  <path
    d="M30 70
       C20 140, 60 120, 90 100
       C120 80, 150 60, 70 30"
    stroke={color}
    stroke-width="24"
    stroke-linecap="round"
    stroke-linejoin="round"
    fill="none"
  />
</svg>

  