<template>
  <div>
    <header class="header" :class="{sticky: $route.path === '/'}">
      <div class="container">
        <div class="left">
          <g-link :to="{ name: 'home' }" class="home-link">
            <img
              src="../../static/logo.svg"
              :alt="settings.site_name"
              class="logo"
              width="60px"
              height="24px"
            />
            </g-link>
        </div>
        <nav class="nav right">
          <g-link class="nav__link" to="/journal">Journal</g-link>
          <g-link class="nav__link" to="/contact">Say Hi!</g-link>
        </nav>
      </div>
    </header>
    <!--
      La directive `v-for` : https://fr.vuejs.org/v2/api/#v-for
      Nous permet ici de créer une boucle itérative sur les notifications
    -->
    <div v-for="notification in settings.notifications" :key="notification.id">
      <!--
        Pour chaque entrée de `notifications` un composant est crée,
        la données de notification est passé au composant via `v-bind`.
        Documentation sur `v-bind`: https://fr.vuejs.org/v2/api/#v-bind
      -->
      <Notification
        v-bind:notification="notification"
      />
    </div>
  </div>
</template>

<script>
import Notification from '@/components/Elements/Notification.vue'

export default {
  components: {
    Notification
  },
  data() {
    return {
      logo: require("../../static/logo.svg"),
      settings: require("../../data/theme.json")
    }
  }
}
</script>

<style scoped>
.header {
  position: relative;
  height: 6rem;
  z-index: 10;
}
.header.sticky {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
.header > .container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
.home-link {
  text-decoration: none;
}
.logo {
  height: 1.5rem;
}
.site-name {
  font-size: 0.9em;
  font-weight: 700;
  letter-spacing: 0.05em;
  text-decoration: none;
  text-transform: uppercase;
}
.nav > * {
  font-size: 0.9  em;
  font-weight: 600;
  text-decoration: none;
  margin-top: 4px;
  margin-right: 3rem;
  padding-bottom: 4px;
  border-bottom: 1px solid;
  border-color: transparent;
  transition: border 0.15s;
}
.nav > *:last-of-type {
  margin: 0;
}
.nav > *:hover {
  border-color: inherit;
}
.nav > .active {
  border-color: inherit;
}
</style>
