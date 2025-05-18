<!-- SwooshIcon.svelte -->
<script>
    export let size = 64;
    export let color = "#009688"; // verde petróleo
  </script>
  
  <svg
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 100 100"
    width={size}
    height={size}
    fill="none"
  >
    <path
      d="M70 10
         C50 30, 50 40, 70 60
         C90 80, 60 90, 40 80
         C20 70, 30 40, 30 20"
      stroke={color}
      stroke-width="16"
      stroke-linecap="round"
      stroke-linejoin="round"
      fill="none"
    />
  </svg>