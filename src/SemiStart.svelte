<script>
  export let commits = 0;
  export let maxCommits = 200;
  const maxStars = 15;

  const numStars = Math.max(1, Math.round((commits / maxCommits) * maxStars));
  const radius = 80;
  const centerX = 100;
  const centerY = 100;

  const stars = Array.from({ length: numStars }, (_, i) => {
    const angle = Math.PI * (i / (numStars - 1 || 1)); // evita NaN si solo hay 1 estrella
    return {
      x: centerX + radius * Math.cos(angle),
      y: centerY - radius * Math.sin(angle)
    };
  });
</script>

<svg width="300" height="220" viewBox="0 0 200 120" xmlns="http://www.w3.org/2000/svg">
  {#each stars as star}
    <g transform="translate({star.x}, {star.y})">
      <path
        d="M10 1 L12 7 H18 L13 11 L15 17 L10 13 L5 17 L7 11 L2 7 H8 Z"
        fill="none"
        stroke="#ccc"
        stroke-width="1.5"
        transform="scale(0.8) translate(-10, -10)"
      />
    </g>
  {/each}
</svg>
