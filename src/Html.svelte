<!-- LoopyStrokeIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#f03800"; // rojo intenso
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
    d="M90 20
       C50 30, 30 30, 50 50
       C70 70, 30 70, 30 90"
    stroke={color}
    stroke-width="10"
    stroke-linecap="round"
    stroke-linejoin="round"
    fill="none"
  />
</svg>