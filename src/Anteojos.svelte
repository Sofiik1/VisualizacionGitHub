<script>
  export let color = "black";
</script>

<svg width="100" height="100">
  <circle cx="35" cy="50" r="10" stroke={color} stroke-width="3" fill="none" />
  <circle cx="65" cy="50" r="10" stroke={color} stroke-width="3" fill="none" />
  <line x1="45" y1="50" x2="55" y2="50" stroke={color} stroke-width="3" />
</svg>

<style>
  svg {
    position: absolute;
    top: 15%;
    left: 10%;
    pointer-events: none;
  }
</style>

