<template>
    <div class="hero">
        <h1 class="hero-title" v-html="settings.hero_title" />
        <h2 class="hero-subtitle" v-html="settings.hero_subtitle" />
        <!--
          Appel du composant, des propriétés (Props) peuvent êtres passé au composant (ici `href` et `class`).
          Notez que le contenu "Lire cet article" est une donnée passé via un Slot.
          Documentation sur les slots : https://fr.vuejs.org/v2/guide/components.html#Distribution-de-contenu-avec-les-slots
          Documentation sur les Props : https://fr.vuejs.org/v2/guide/components-props.html#Passage-de-props-statiques-ou-dynamiques
        -->
        <Button
          href="/journal/gridsome-forestry-cms"
          class="is-dark"
        >Lire cet article</Button>
    </div>
</template>

<script>
// Importez votre composant ici, l'extension `.vue` n'est pas nécesaire.
import Button from '@/components/Elements/Button'

export default {
  // Vous déclarer vos composants ici.
  components: {
    Button
  },
  data() {
    return {
      settings: require("../../data/theme.json")
    }
  }
}
</script>

<style>
.hero {
    text-align: center;
    width: 80%;
    max-width: 100%;
    margin: 0 auto;
    padding: 4rem 0 8rem 0;
}

.hero-title {
    font-size: 3em;
    font-weight: 700;
    padding: 0;
    margin: 0 0 2rem 0;
}
.hero-title p,
.hero-subtitle p {
    color: var(--color-contrast-1);
    margin: 0;
    padding: 0;
}
.hero-subtitle {
    font-weight: 400;
    font-style: italic;
    line-height: 1.3em;
    padding: 0;
}
</style>
