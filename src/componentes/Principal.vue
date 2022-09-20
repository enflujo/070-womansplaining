<script setup>
import podcast from '../recursos/episodios.json';
</script>

<template>
  <div id="contenedorGeneral">
    <header>
      <h1>Womansplaining</h1>
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

#contenedorGeneral {
  border: none;
  margin: 0;
  padding: 2em;
  background-color: rgb(255, 80, 80);
}

#subtitulo {
  padding: 0 12vw;
  font-size: 1.1em;
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
