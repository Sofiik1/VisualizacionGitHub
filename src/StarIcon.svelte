<!-- StarIconRounded.svelte -->
<script>
  export let size = 64;
  export let color = "#cc66d9";
  export let strokeWidth = 6;
  export let style = "";
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 100 100"
  width={size}
  height={size}
  fill="none"
  stroke={color}
  stroke-width={strokeWidth}
  stroke-linejoin="round"
  stroke-linecap="round"
  style={style}
>
  <path d="
    M50 10 
    L61 39 
    L92 39 
    L66 59 
    L76 89 
    L50 70 
    L24 89 
    L34 59 
    L8 39 
    L39 39 
    Z" />
</svg>