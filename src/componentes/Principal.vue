<script setup>
import { onMounted, ref } from 'vue';

const datosPodcast = ref(null);
const datosEpisodios = ref(null);
const episodioActual = ref('');
const base = 'https://api.spotify.com/v1/shows/3VaDJUfiay01QnqyEj1FVU';
const token = ''; // Generar token en https://developer.spotify.com/console/shows/
const opciones = {
  method: 'GET',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
    Authorization: `Bearer ${token}`,
  },
};

onMounted(async () => {
  datosPodcast.value = await fetch(`${base}`, opciones).then((respuesta) => respuesta.json());
  datosEpisodios.value = await fetch(`${base}/episodes`, opciones).then((respuesta) => respuesta.json());
  // console.log(datosEpisodios.value.items[0].external_urls.spotify);
});
</script>

<template>
  <div id="contenedorGeneral">
    <header>
      <h1>Womansplaining</h1>
      <p id="subtitulo" v-if="datosPodcast">
        Un podcast de <a href="https://cerosetenta.uniandes.edu.co/">070</a> con Gloria Susana Esquivel: conversaciones
        sobre género en diferentes campos de la sociedad y la cultura. Producido por su anfitriona Gloria Susana
        Esquivel y editado por Goldy Levy.
      </p>
    </header>

    <div class="episodios" v-if="datosEpisodios">
      <div class="elemento" v-for="(episodio, i) in datosEpisodios.items" :key="`episodio${i}`">
        <iframe
          class="iframe"
          :key="`nivel${i}`"
          style="border-radius: 12px"
          :src="`https://open.spotify.com/embed/episode/${episodio.id}?utm_source=generator&theme=0`"
          width="100%"
          height="250"
          frameBorder="0"
          allowfullscreen=""
          allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
          loading="lazy"
        ></iframe>
        <!--  <a :href="`${episodio.external_urls.spotify}`" target="_blank"
          ><img class="imagen" :src="`${episodio.images[0].url}`"
        /></a> -->
        <p class="descripcion">{{ episodio.description }}</p>
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

.descripcion {
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  display: -webkit-box;
  margin: 0px 0 15px 0px;
  overflow: hidden;
  padding: 0;
  word-break: break-word;
  width: 15vw;
}

.imagen {
  width: 15vw;
}

.elemento {
  margin: 1em 1em 0em 2em;
}
</style>
