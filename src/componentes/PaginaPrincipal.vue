<script setup>
import { onUnmounted, onMounted, ref } from 'vue';
let animador;
let creditosVisibles = ref(false);

onMounted(() => {
  const stageW = window.innerWidth;
  const stageH = window.innerHeight;
  const centerX = stageW / 2;
  const centerY = stageH / 2;
  const svg = document.getElementById('trenza');
  const amps = [];
  const numeroOndas = 100;

  const limite = 500;

  for (let i = 0; i < numeroOndas; i++) {
    const path = document.createElementNS('http://www.w3.org/2000/svg', 'path');
    const amp = i * 10;

    const d = `M 0 ${centerY} C ${centerX - centerX / 2} ${centerY - amp} ${centerX + centerX / 2} ${
      centerY + amp
    } ${stageW} ${centerY} `;

    svg.setAttribute('viewBox', '0, 0, ' + stageW + ', ' + stageH);
    path.setAttributeNS(null, 'd', d);
    svg.appendChild(path);

    amps.push([1, amp]);
  }
  const lineas = svg.querySelectorAll('path');

  function loop() {
    lineas.forEach((linea, i) => {
      let ampY = amps[i][1];
      let direction = amps[i][0];

      ampY = ampY + 1 * direction;

      if (ampY > limite) {
        amps[i][0] = -Math.random();
      } else if (ampY < -limite) {
        amps[i][0] = Math.random();
      }

      linea.setAttributeNS(
        null,
        'd',
        `M 0 ${centerY} C ${centerX - centerX / (2 * (i + 1))} ${centerY - ampY} ${centerX + centerX / (2 * (i + 1))} ${
          centerY + ampY
        } ${stageW} ${centerY} `
      );

      amps[i][1] = ampY;
    });

    animador = requestAnimationFrame(loop);
  }

  loop();
});

onUnmounted(() => {
  cancelAnimationFrame(animador);
});

function mostrarCreditos() {
  creditosVisibles.value = !creditosVisibles.value;
}
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
        Esto es Womansplaining. Un Podcast de <a href="https://cerosetenta.uniandes.edu.co/" target="_blank">070</a> con
        Gloria Susana Esquivel y Lina Vargas, editado por Goldy Levy.
        <br />
        Tenemos conversaciones sobre feminismo, arte, política y cultura.
      </p>
    </header>

    <iframe
      id="reproductor"
      style="border-radius: 12px"
      src="https://open.spotify.com/embed/playlist/665f5UiNYieTeswi9OMazI?utm_source=generator&theme=0"
      frameBorder="0"
      allowfullscreen=""
      allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
      loading="lazy"
    ></iframe>

    <svg id="trenza" version="1.1" xmlns="http://www.w3.org/2000/svg"></svg>

    <div @click="mostrarCreditos()" id="botonCreditos">?</div>
  </div>

  <div id="creditos" :class="creditosVisibles ? 'activo' : ''">
    <div id="cerrarCreditos" @click="mostrarCreditos()">X</div>
    <h1>Womansplaining</h1>
    <p>Un podcast de <a href="https://cerosetenta.uniandes.edu.co/" target="_blank">070</a></p>

    <h3>Equipo</h3>

    <ul class="equipo">
      <li class="persona">
        <div class="rol">Producción</div>
        <div class="nombre">Gloria Susana Esquivel y Lina Vargas</div>
      </li>
      <li class="persona">
        <div class="rol">Edición</div>
        <div class="nombre">Goldy Levy</div>
      </li>
      <li class="persona">
        <div class="rol">Desarrollo web</div>
        <div class="nombre"><a href="https://enflujo.com/" target="_blank">Laboratorio EnFlujo</a></div>
      </li>
    </ul>
    <div id="logos">
      <a href="https://enflujo.com/" target="_blank"><img src="../assets/imgs/logoEnflujo.svg" alt="Logo EnFlujo" /></a>

      <a href="https://cerosetenta.uniandes.edu.co/" target="_self"
        ><img src="../assets/imgs/logo070.png" alt="Logo Cerosetenta"
      /></a>
    </div>
  </div>
</template>
.

<style lang="scss">
body {
  overflow: hidden;
  background-color: #282828;
  a {
    color: #20c594;
    text-decoration: none;
    font-weight: bold;
  }
  a:hover {
    color: #ff3d42;
  }
}
header {
  text-align: center;
  width: 100vw;
}

#contenedorGeneral {
  border: none;
  margin: 0;
  min-height: 100vh;

  ::selection {
    background: #20c594;
  }
}

#reproductor {
  margin: 0 auto;
  display: block;
  width: 80%;
  height: 135vh;
  overflow: hidden;
}

#imagenes {
  background-color: white;
}

#imagen1 {
  display: none;
}

#imagen2 {
  position: relative;
}

.imagen {
  background-color: white;
  position: relative;
  top: 0px;
  display: flex;
}

.persona {
  margin-bottom: 1em;
}

.rol {
  font-weight: bold;
}

@keyframes pasarLogo {
  0% {
    left: 150%;
  }

  100% {
    left: -150%;
  }
}

.logo {
  position: relative;
  width: 90vw;
  margin: 1em auto;
}

#imagen1 {
  left: 100%;
  visibility: hidden;
}

#subtitulo {
  padding: 1em 20vw 0em;
  font-size: 1em;
  color: white;
}

#creditos {
  position: absolute;
  top: 0;
  left: 0;
  background-color: white;
  width: 100vw;
  height: 100vh;
  padding: 5%;
  visibility: hidden;

  &.activo {
    visibility: visible;
  }
}

#cerrarCreditos {
  cursor: pointer;

  &:hover {
    color: #20c594;
  }
}

#botonCreditos {
  position: absolute;
  bottom: 10px;
  right: 55px;
  color: white;
  cursor: pointer;

  &:hover {
    color: #20c594;
  }
}

#logos {
  display: inline-block;
  margin: 31px 10px;

  img {
    height: 27px;
    margin: 0 20px;
  }
}

// Pantallas grandes
@media (min-width: 1200px) {
  #subtitulo {
    padding: 1.5em 20vw 1em;
    font-size: 1.2em;
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
    margin: 0;
  }

  #imagen1 {
    animation: pasarLogo 20s 0s linear infinite;
    left: 100%;
    visibility: visible;
  }

  #imagen2 {
    animation: pasarLogo 20s 10s linear infinite;
    left: 100%;
  }

  #reproductor {
    margin: 0 auto;
    display: block;
    width: 50%;
    height: 55vh;
  }
}

// Tablet
@media (min-width: 768px) {
  #subtitulo {
    padding: 1.5em 15vw 1em;
    font-size: 1.2em;
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
    margin: 0;
  }

  #imagen1 {
    animation: pasarLogo 20s 0s linear infinite;
    left: 100%;
    visibility: visible;
    display: block;
  }

  #imagen2 {
    animation: pasarLogo 20s 10s linear infinite;
    left: 100%;

    position: absolute;
    width: 100vw;
  }
}

#trenza {
  position: absolute;
  top: 0;
  opacity: 0.2;
  pointer-events: none;
}

path {
  fill: transparent;
  stroke: rgb(27, 243, 45);
  stroke-width: 0.5px;
  position: absolute;
}

#reproductor {
  margin: 0 auto;
  display: block;
  width: 80%;
  height: 55vh;
}
</style>
