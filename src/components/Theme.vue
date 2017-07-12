<template>
  <div class="theme">
    <h3>{{ theme_id }}. {{ themes[theme_id].name }}</h3>
    <div class="filters">
      <router-link :to="{path: `/${theme_id}/${i + 1}`}" v-for="(subtheme, i) in themes[theme_id -1].subthemes">
        <v-chip v-bind:class="{red: i == (subtheme_id -1)}" class="primary white--text" >{{theme_id}}.{{i + 1}}. {{ subtheme.name }}
        </v-chip>
      </router-link>
    </div>
    <div class="subfilters">
        <v-chip v-for="(subtheme, i) in themes[theme_id - 1].subthemes[subtheme_id - 1].subthemes" v-bind:class="{red: i == (subtheme_id -1)}" class="primary white--text" > {{ subtheme.name }}
        </v-chip>
    </div>
  </div>
</template>

<script>

import themes from '../themes/'

export default {
  name: 'theme',
  props: ['theme_id', 'subtheme_id'],
  data () {
    return {
      themes: themes
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
