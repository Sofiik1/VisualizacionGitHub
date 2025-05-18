<!-- CurvedAbstractIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#8bc34a"; // verde lima
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
    d="M20 100
       C20 110, 10 90, 30 80
       C60 80, 60 90, 80 75
       C90 60, 90 40, 60 50
       C40 60, 20 40, 10 20"
    fill="none"
    stroke={color}
    stroke-width="10"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>