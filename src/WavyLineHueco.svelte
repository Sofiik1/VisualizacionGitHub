<script>
  export let size = 64;
  export let color = "#fe1492";
<<<<<<< HEAD
  export let strokeWidth = 6;
  export let style = "";
=======
  export let style = "";
  export let viewBox = "0 0 20 300";
  export let strowidth = 6;
>>>>>>> fork/master
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
<<<<<<< HEAD
  viewBox="0 0 20 300"
=======
  viewBox={viewBox}
>>>>>>> fork/master
  width={size}
  height={size}
  style={style}
  fill="none"
>
  <path
    d="M10 0
       Q 0 15, 10 30
       Q 20 45, 10 60
       Q 0 75, 10 90
       Q 20 105, 10 120
       Q 0 135, 10 150
       Q 20 165, 10 180
       Q 0 195, 10 210
       Q 20 225, 10 240
       Q 0 255, 10 270
       Q 20 285, 10 300"
    stroke={color}
<<<<<<< HEAD
    stroke-width={strokeWidth}
=======
    stroke-width={strowidth}
>>>>>>> fork/master
    stroke-dasharray="10 10"  
    stroke-linecap="round"
  />
</svg>
