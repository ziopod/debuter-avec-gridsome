<template>
  <!-- 
    La propriété dynamique `color` est passé à l'attribut HTML `class` 
    via le shorthand `v-bind`.
    `v-show` affiche ou non le composant en focntion de l'état de `isActive`.
    Documenation sur `v-show` : https://vuejs.org/v2/api/#v-show
  -->
  <div class="message" v-bind:class="notification.color" v-show="isActive">
    {{ notification.message }}
    <!--
      Le bouton de fermeture de notification est gérée sous forme de composant
      La directive `v-on` est utilisée pour écouter l'évenement HTML de click sur le bouton, ce click déclenchetra la fonction `close()`.
      Documentation sur `v-on` : https://fr.vuejs.org/v2/api/#v-on
      Documentation sue les écouteurs d'évenement HTML : https://developer.mozilla.org/fr/docs/Web/API/EventListener
    -->
    <Close v-on:click.native="close()" />
  </div>
</template>
<script>
import Close from '@/components/Elements/Close.vue'

export default {
  props: {
    notification: {
      type: Object,
      required: true
    }
  },
  components: {
    Close
  },
  data() {
    return {
      /* Déclaration de l'état de l'affichage pour ce composant */
      isActive: false
    }
  },
  mounted() {
    /**
     * Lecture du stockage local du navigateur et attribution de la valeur
     * à `isActive`
     */
    this.isActive = localStorage.getItem(`notification-${this.notification.id}is-active`) !== 'false'
  },
  methods: {
    /**
     * Méthode de fermeture de la notification
     * Documentation sur les métodes : https://fr.vuejs.org/v2/api/index.html#methods
     */
    close() {
      this.isActive = false
      // Enregistrement de l'état dans le stokage local
      localStorage.setItem(`notification-${this.notification.id}-is-active`, this.isActive)
    }
  }
}
</script>
<style scoped>
.message{
  display: flex;
  justify-content: space-between;
  background-color: rgb(245, 245, 245);
  padding: 1em;
}
.message.is-warning {
  color: black;
  background-color: rgb(255, 221, 87);
}
.message.is-info {
  color: white;
  background: rgb(50, 152, 220);
}
</style>