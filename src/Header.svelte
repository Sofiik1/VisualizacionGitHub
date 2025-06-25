<script>
  import { FaGithub, FaProjectDiagram, FaUsers, FaNetworkWired, FaChartBar } from 'svelte-icons/fa';
</script>

<style>
.header {
    display: flex;
    justify-content: center;
    background-color: #0d1117;
    max-height: 10vh;
    color: #c9d1d9; 
    padding: 3rem;
    font-family: sans-serif;
    border-bottom: 1px solid #30363d;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 3px;
    font-family: "Electrolize", sans-serif;
    font-size: 1rem;
    color: #ffffff;
    text-align: center;
  }

  .nav {
    display: flex;
    gap: 24px;
    margin-left: 30%;
    font-size: 1rem;
    color: #ffffff;
    line-height: 1.2;
    text-align: center;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 6px;
    cursor: pointer;
    color: #c9d1d9;
    padding: 4px 8px;
    border-radius: 4px;
  }

  .nav-item:hover {
    background-color: #21262d;
  }

  .spacer {
    flex-grow: 1;
  }

  .icono-logo{
    height: 80px;
    width: 150px;
  }

  .nav-item .icono{
    height: 30px;
    width: 30px;
  }

</style>

<header>
<div class="header">
  <div class="logo">
    <div class="icono-logo">
        <FaGithub style="width: 40px; height: 40px;"/>
    </div>
    <span><strong>TD-Ditella /</strong> Repos de la carrera</span>
  </div>

  <nav class="nav">
  <a class="nav-item" href="#red">
    <span class="icono"><FaNetworkWired /></span>
    <span>Red</span>
  </a>
  <a class="nav-item" href="#colaboradores">
    <span class="icono"><FaUsers /></span>
    <span>Colaboradores</span>
  </a>
  <a class="nav-item" href="#repositorios">
    <span class="icono"><FaProjectDiagram /></span>
    <span>Repositorios</span>
  </a>
  <a class="nav-item" href="#insights">
    <span class="icono"><FaChartBar /></span>
    <span>Insights</span>
  </a>
</nav>


  <div class="spacer"></div>
</div>
</header>
