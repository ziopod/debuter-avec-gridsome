<template>
  <a class="button">
    <!--
      Le contenu passé via le Slot sera affiché ici.
      Notez qu'il est possible d'ajouter un conteun standard (ici la flêche "❯")
    -->
    <slot/> ❯
  </a>
</template>

<style>
/* Définir le CSS resérvé au composant ici */
.button {
  display: inline-block;
  text-transform: uppercase;
  text-decoration: none;
  padding: .75em 1em;
}
.is-dark {
  background: black;
  color: white;
}
</style>