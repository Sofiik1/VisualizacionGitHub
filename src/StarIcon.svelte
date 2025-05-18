<!-- StarIcon.svelte -->
<script>
    export let size = 64;
    export let color = "#cc66d9"; // violeta pastel
    export let style = "";
    </script>
  
  <svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 100 100"
  width={size}
  height={size}
  fill={color}
  style={style}
  >
    <polygon
      points="50,10 61,39 92,39 66,59 76,89 50,70 24,89 34,59 8,39 39,39"
    />
  </svg>
  