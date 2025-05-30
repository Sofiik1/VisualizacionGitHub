<!-- CurvedAbstractIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#8bc34a"; // verde lima
  export let style = "";
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="10 0 100 100"
  width={size}
  height={size}
  fill="none"
  style={style}
>
  <path
    d="M-20 100
       C30 110, 20 80, 50 75
       C70 80, 90 100, 90 75
       C90 60, 70 50, 60 50
       C50 70, 30 60, 10 20"
    fill="none"
    stroke={color}
    stroke-width="9"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>