<script setup>
import podcast from '../assets/episodios.json';
</script>

<template>
  <div id="contenedorGeneral">
    <header>
      <div id="imagenes">
        <div id="imagen1" class="imagen">
          <img id="logoUno" class="logo" src="../assets/imgs/womansplaining-logo.png" />
        </div>
        <div id="imagen2" class="imagen">
          <img id="logoTres" class="logo" src="../assets/imgs/womansplaining-logo.png" />
        </div>
      </div>
      <p id="subtitulo">
        Un podcast de <a href="https://cerosetenta.uniandes.edu.co/">070</a> con Gloria Susana Esquivel: conversaciones
        sobre género en diferentes campos de la sociedad y la cultura. Producido por su anfitriona Gloria Susana
        Esquivel y editado por Goldy Levy.
      </p>
    </header>

    <div class="episodios" v-if="podcast">
      <div class="elemento" v-for="(episodio, i) in podcast.episodios" :key="`episodio${i}`">
        <iframe
          v-if="episodio.codigo"
          class="iframe"
          :key="`nivel${i}`"
          style="border-radius: 12px"
          :src="`https://open.spotify.com/embed/episode/${episodio.codigo}?utm_source=generator&theme=0`"
          width="100%"
          height="250"
          frameBorder="0"
          allowfullscreen=""
          allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
          loading="lazy"
        ></iframe>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
header {
  text-align: center;
}

#imagenes {
  background-color: white;
}

#contenedorGeneral {
  border: none;
  margin: 0;
  background-color: #ff3d42;
}

.imagen {
  background-color: white;
  position: relative;
  top: -10px;
  display: flex;
}

@keyframes pasarLogo {
  0% {
    left: 100%;
  }

  100% {
    left: -100%;
  }
}

.logo {
  position: relative;
  width: 100vw;
}

#imagen1 {
  background-color: red;
  animation: pasarLogo 20s 0s linear infinite;
  left: 100%;
}

#imagen2 {
  animation: pasarLogo 20s 10s linear infinite;
  left: 100%;
  position: absolute;
}

#subtitulo {
  padding: 1em 20vw;
  font-size: 1.2em;
}

.episodios {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.elemento {
  margin: 1em 1em 0em 2em;
}
</style>
