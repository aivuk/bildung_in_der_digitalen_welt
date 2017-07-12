<template>
  <v-app light>
    <v-navigation-drawer
      class="elevation-4"
      persistent
      :mini-variant="miniVariant"
      :clipped="clipped"
      v-model="drawer"
      enable-resize-watcher
    >
    <v-expansion-panel expand>
      <v-expansion-panel-content v-model="openTheme[i]" v-bind:class="{'darken-4': openTheme[i]}" class="teal white--text elevation-3" v-for="(theme, i) in themes" :key="i" ripple>
        <div slot="header">
          <div v-ripple="{ class: 'grey--text' }">{{i + 1}}. {{ theme.name }}</div>
        </div>
        <v-card v-bind:class="{'grey lighten-3 elevation-2': (i == (theme_id - 1)) && (j == (subtheme_id - 1))}" v-for="(subtheme, j) in theme.subthemes" :key="j">
          <v-card-text>
            <router-link :to="{path: `/${i + 1}/${j+1}`}">{{i + 1}}.{{j + 1}}. {{ subtheme.name }} </router-link>
          </v-card-text>
        </v-card>
      </v-expansion-panel-content>
      <v-divider></v-divider>
    </v-expansion-panel>
    </v-navigation-drawer>
    <v-toolbar fixed>
      <v-toolbar-side-icon @click.native.stop="drawer = !drawer" light></v-toolbar-side-icon>
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <main>
      <v-container fluid>
        <theme :theme_id="theme_id" :subtheme_id="subtheme_id"></theme>
        <v-slide-y-transition mode="out-in">
          <v-layout row-sm column child-flex align-center>
            <v-flex v-for="i in 6" :key="i">
              <v-card>
                <v-card-media
                  class="white--text"
                  height="200px"
                  src="https://vuetifyjs.com/static/doc-images/cards/docks.jpg"
                >
                  <v-container fill-height fluid>
                    <v-layout fill-height>
                      <v-flex xs12 align-end flexbox>
                        <span class="headline">Top 10 Australian beaches</span>
                      </v-flex>
                    </v-layout>
                  </v-container>
                </v-card-media>
                <v-card-title>
                  <div>
                    <span class="grey--text">Number 10</span><br>
                    <span>Whitehaven Beach</span><br>
                    <span>Whitsunday Island, Whitsunday Islands</span>
                  </div>
                </v-card-title>
                <v-card-actions>
                  <v-btn flat class="orange--text">Share</v-btn>
                  <v-btn flat class="orange--text">Explore</v-btn>
                </v-card-actions>
              </v-card>
            </v-flex>
          </v-layout>
        </v-slide-y-transition>
      </v-container>
    </main>
  </v-app>
</template>

<script>

  import Theme from './components/Theme'
  import themes from './themes/'

  export default {
    props: ['theme_id', 'subtheme_id'],
    watch: {
      '$route' (to, from) {
        console.log(to, from)
      }
    },
    beforeRouteUpdate (to, from, next) {
      // react to route changes...
      // don't forget to call next()
      console.log(to, from)
      next()
    },
    beforeMount () {
      this.openTheme[this.theme_id - 1] = true
    },
    data () {
      return {
        clipped: false,
        drawer: true,
        fixed: false,
        openTheme: Array(themes.length),
        themes: themes,
        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Bildung in der digitalen Welt'
      }
    },
    components: {
      'theme': Theme
    }
  }
</script>

<style lang="stylus">
  @import './stylus/main'
</style>
