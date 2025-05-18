<!-- DoubleDiamondIcon.svelte -->
<script>
  export let size = 64;
  export let color1 = "#add8e6"; // celeste claro
  export let color2 = "#1565c0"; // azul fuerte
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
  <!-- Primer rombo -->
  <rect
    x="20" y="20"
    width="40" height="40"
    transform="rotate(45 40 40)"
    stroke={color1}
    stroke-width="10"
    fill="none"
    rx="4"
  />

  <!-- Segundo rombo encima -->
  <rect
    x="40" y="40"
    width="20" height="20"
    transform="rotate(45 50 50)"
    stroke={color2}
    stroke-width="10"
    fill="none"
    rx="2"
  />
</svg>