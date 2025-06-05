<script>
  export let color = "#ccc";
  export let width = 60;
</script>


<svg {width} height="6">
  <path
    d="M0,0 Q40,6 {width},0"
    stroke={color}
    stroke-width="3"
    stroke-linecap="round"
    fill="none"
  />
</svg>


<style>
  svg {
    border-radius: 3px;
    filter: drop-shadow(0 1px 1px rgba(0, 0, 0, 0.3));
    display: block;
  }
</style>