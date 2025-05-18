<!-- SwooshIcon.svelte -->
<script>
    export let size = 64;
    export let color = "#009688"; // verde petróleo
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
      d="M90 0
         C50 30, 50 40, 70 60
         C80 80, 60 90, 40 80
         C35 80, 0  40, -20  90"
      stroke={color}
      stroke-width="10"
      stroke-linecap="round"
      stroke-linejoin="round"
      fill="none"
    />
  </svg>