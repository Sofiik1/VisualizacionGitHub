<!-- ZigzagIcon.svelte -->
<script>
  export let size = 64;
  export let color = "#ff8acb"; // naranja vibrante "#ec4899"
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
    d="M5 10 
    L55 30 
    L50 55 
    L95 90"
    stroke={color}
    stroke-width="12"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>