<template>
  <!-- Passer la propriété dynamique `color` à l'attribut HTML `class` -->
  <!-- Shorthand de `v-bind` : `:` -->
  <div class="message" v-bind:class="notification.color" v-show="isActive">
    {{ notification.message }}
    <!-- Sous forme de composant -->
    <!-- Shorthand de `v-on` : `@` -->
    <!-- <Close v-on:click.native="isActive = !isActive" /> -->
    <Close v-on:click.native="toggle()" />
    <!-- <button
      class="close"
      aria-label="close"
      @click="isActive = !isActive"
    ></button> -->
  </div>
</template>
<script>
/**
 * Étapes : 
 * 1. créer le composant `Elements/Notification.vue` avec son CSS
 * 2. ajouter la propriété `message` en statique
 * 3. ajouter la variante de style `is-danger`
 * 4. appliquer la variante avec la propriété dynamyque `color`
 * 5. créer le bouton close (sans CSS) avec sont interaction
 * 6. passer le bouton sous forme de composant pour gérer la stylisation
 */
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
      isActive: true,
      uid: null
    }
  },
  mounted() {
    this.isActive = localStorage.getItem(`notification-${this.notification.id}`) !== 'false'
  },
  methods: {
    toggle() {
      this.isActive = !this.isActive
      localStorage.setItem(`notification-${this.notification.id}`, this.isActive)
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
  background-color: rgb(255, 221, 87);
}
.message.is-info {
  color: white;
  background: rgb(50, 152, 220);
}
</style>