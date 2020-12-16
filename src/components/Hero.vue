<template>
    <div class="hero">
        <h1 class="hero-title" v-html="settings.hero_title" />
        <h2 class="hero-subtitle" v-html="settings.hero_subtitle" />
        <a href="/journal/gridsome-forestry-cms" class="buton" style="
        display: inline-block;
        background: black;
        color: white;
        text-transform: uppercase;
        text-decoration: none;
        padding: 1em;
        float: right;
        ">
          Call to action
        </a>
    </div>
</template>

<script>
export default {
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
