<template>
  <div class="layout" :class="{ 'sticky-header': $route.path === '/' }">
       <!-- Passer une propriété dynamique `message` -->
      <!-- Directive Vue `v-bind` -->
      <!-- Bind = attacher en FR -->
      <!-- Passer une propriété statique `color` -->
      <div v-for="notification in settings.notifications" :key="notification.id">
        <Notification
          v-bind:notification="notification"
        />
      </div>
    <Header />
    <slot/>
    <Footer />
  </div>
</template>

<script>
import Header from "@/components/Header"
import Footer from "@/components/Footer"
/**
 * La définition du message ici est utile que
 * si l'on veut exploiter du code logique.
 * Par exemple, récupérer un message définie via le CMS.
 * cf. `settings.json` dans `components/Header.vue`
 * 
 * Techniquement, on pourrait également gérer la couleur depuis le CMS,
 * permettre l'écriture du message au format HTML, afficher plusieurs;
 * notifications, "zoner" les notification, etc.
 * 
 */
import Notification from '@/components/Elements/Notification.vue'

export default {
  components: {
    Header,
    Footer,
    Notification
  },
  data() {
    return {
      settings: require('../../data/theme.json'),
      message: "Une simple message : Salut! 😃"
    }
  }
}
</script>


<style>
* {
  box-sizing: border-box;
}
@font-face {
  font-family: "PT Serif";
  /* Éviter l'invisibilté de la fonte : https://web.dev/avoid-invisible-text */
  font-display: auto;
  src: local('PT Serif'), url('https://fonts.googleapis.com/css2?family=PT+Serif:wght@700&display=swap') format('woff2');
}
@font-face {
  font-family: "PT Sans";
  /* Comment choisir le paramètre de font-display : https://developers.google.com/web/updates/2016/02/font-display */
  font-display: fallback;
  src: local('PT Sans'), url('https://fonts.googleapis.com/css2?family=PT+Sans:ital,wght@0,400;0,700;1,400&display=swap') format('woff2');
}
body {
  --color-base: rgb(255, 255, 255);
  --color-base-1: rgb(243, 243, 243);
  --color-contrast: rgb(0, 0, 0);
  --color-contrast-1: rgb(43, 43, 43);
  --font-size: 1em;
  font-family:  "PT Sans", Arial, sans-serif;
  margin:0;
  padding: 0;
  font-size: var(--font-size);
  line-height: 1.5em;
  background: var(--color-base);
  color: var(--color-contrast);
  transition: background 0.5s ease;
}

body.dark {
  --color-base: rgb(0, 0, 0);
  --color-base-1: rgb(43, 43, 43);
  --color-contrast: rgb(255, 255, 255);
  --color-contrast-1: rgb(243, 243, 243);
}

h1 {
  font-family: "PT Serif", Georgia, serif;
  text-transform: uppercase;
  line-height: 1.3em;
}

p {
    line-height: 1.5;
    font-size: 1.15em;
}

.layout {
  padding: 0;
}

.layout.sticky-header {
  padding: 6rem 0 0 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (min-width: 860px) {
  body {
    --font-size: 1.312em;
  }
  .container {
    padding: 0 6rem;
  }
}

a {
  color: inherit;
}

img {
  max-width: 100%;
}

.label {
  display: block;
  font-weight: 700;
  margin-bottom: 0.5rem;
}
</style>
