<script>
  export let color = "#e5e4e2"; // Platinum tone
  export let width = 53;
</script>

<svg {width} height="15" class="platinum-svg">
  <!-- Black border path (slightly thicker and rendered first) -->
  <path
    d="M0,5 Q30,10 {width},5"
    stroke="black"
    stroke-width="10"
    stroke-linecap="round"
    fill="none"
  />
  
  <!-- Platinum path (on top) -->
  <path
    d="M0,5 Q30,10 {width},5"
    stroke={color}
    stroke-width="8"
    stroke-linecap="round"
    fill="none"
  />
</svg>

<style>
  .platinum-svg {
    display: block;
    filter: drop-shadow(0 1px 1px rgba(0, 0, 0, 0.3));
  }
</style>