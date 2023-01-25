<script setup>
import { onUnmounted, onMounted } from 'vue';
let animador;

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
        Un podcast de <a href="https://cerosetenta.uniandes.edu.co/" target="blank">070</a> con Gloria Susana Esquivel:
        conversaciones sobre género en diferentes campos de la sociedad y la cultura. Producido por su anfitriona Gloria
        Susana Esquivel y editado por Goldy Levy.
      </p>
    </header>

    <iframe
      id="reproductor"
      style="border-radius: 12px"
      src="https://open.spotify.com/embed/playlist/665f5UiNYieTeswi9OMazI?utm_source=generator&theme=0"
      width="50%"
      height="470px"
      frameBorder="0"
      allowfullscreen=""
      allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
      loading="lazy"
    ></iframe>

    <svg id="trenza" version="1.1" xmlns="http://www.w3.org/2000/svg"></svg>
  </div>

  <div id="creditos"></div>
</template>

<style lang="scss">
body {
  overflow: hidden;
}
header {
  text-align: center;
}

#contenedorGeneral {
  border: none;
  margin: 0;
  background-color: #282828;
  min-height: 100vh;

  ::selection {
    background: #20c594;
  }

  a {
    color: #20c594;
    text-decoration: none;
  }
  a:hover {
    color: #ff3d42;
  }
}

#reproductor {
  margin: 0 auto;
  display: block;
}

#imagenes {
  background-color: white;
}

.imagen {
  background-color: white;
  position: relative;
  top: 0px;
  display: flex;
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

#imagen2 {
  left: 0%;
  position: absolute;
  width: 100vw;
}

#subtitulo {
  padding: 1em 20vw 0em;
  font-size: 1em;
  color: white;
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
  }

  #imagen2 {
    animation: pasarLogo 20s 10s linear infinite;
    left: 100%;
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
</style>
