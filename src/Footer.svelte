<script>
  import { FaGithub} from 'svelte-icons/fa';
</script>

<style>
.footer {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    align-items: center;
    gap: 1rem;
    padding: 3rem;
    background-color: #0d1117;
    height: 10%;
    color: #c9d1d9;
    font-family: sans-serif;
    font-size: 0.9rem;
    border-top: 1px solid #30363d;
  }

footer a {
    color: #ffffff;
    text-decoration: none;
    font-size: 20px;
}

footer a:hover {
    text-decoration: underline;
}


.icono{
    height: 30px;
    width: 30px;
  }

</style>

<footer>
    <div class="footer">
        <a href="https://github.com/ezemaut/VisualizacionFinal" target="_blank" >Repositorio en GitHub</a>
        <span>|</span>
        <div class="icono"><FaGithub style="width: 40px; height: 40px;"/></div>
        <a href="https://www.linkedin.com/in/sofia-kutter" target="_blank">Sofía Kutter</a>
        <span >|</span>
        <div class="icono"><FaGithub style="width: 40px; height: 40px;"/></div>
        <a href="https://www.linkedin.com/in/ezequiel-mautner/" target="_blank">Ezequiel Mautner</a>
        <span>|</span>
         <div class="icono"><FaGithub style="width: 40px; height: 40px;"/></div>
        <a href="https://www.linkedin.com/in/morafernandezstickar/" target="_blank">Mora Fernandez</a>
    </div>

</footer>