<template>
  <v-app>
    <v-card
        color="grey lighten-4"
        flat
        tile
    >
      <v-toolbar dense>
<!--        <v-app-bar-nav-icon></v-app-bar-nav-icon>-->

        <v-toolbar-title>BR Counter</v-toolbar-title>

        <v-spacer></v-spacer>

<!--        <v-btn icon>-->
<!--          <v-icon>mdi-magnify</v-icon>-->
<!--        </v-btn>-->

        <v-btn icon>
          <v-icon>mdi-book-open</v-icon>
        </v-btn>

      </v-toolbar>
    </v-card>

    <v-main>
      <Board/>
    </v-main>
  </v-app>
</template>

<script>
import Board from './components/Board';

export default {
  name: 'App',

  components: {
    Board,
  },

  data: () => ({
    //
  }),
};
</script>
