<template>
  <v-container fluid>
    <v-row dense>
      <v-col
          v-for="card in cards"
          :key="card.title"
          :cols="card.flex"
      >
        <v-card :color="card.color">
          <v-card-title v-text="card.title"></v-card-title>
          <v-divider class="mx-4"></v-divider>

          <v-card-title v-if="card.title === 'ATT'" v-text="scoreHistory[scoreNumber].attack"></v-card-title>
          <v-card-title v-else-if="card.title === 'VOL'" v-text="scoreHistory[scoreNumber].voltage"></v-card-title>
          <v-card-title v-else-if="card.title === 'DEF'" v-text="scoreHistory[scoreNumber].defence"></v-card-title>
          <v-card-title v-else v-text="scoreHistory[scoreNumber].hp"></v-card-title>

          <v-card-actions>
            <v-btn small v-on:click="minus(card.title)">
              <v-icon>mdi-numeric-negative-1</v-icon>
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn small v-on:click="plus(card.title)">
              <v-icon>mdi-plus-one</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>

      <v-col :cols="12">
        <v-card :color="'#607D8B'">
          <v-card-title v-text="'HP'"></v-card-title>
          <v-divider class="mx-4"></v-divider>
          <v-progress-linear
              v-bind:value="scoreHistory[scoreNumber].hp * 6.66"
              color="amber"
              height="25"
          >
            <template v-slot:default="{ value }">
              <strong>{{ Math.round(value/6.66) }}</strong>
            </template>
          </v-progress-linear>
          <v-card-actions>
            <v-btn small v-on:click="minus()">
              <v-icon>mdi-numeric-negative-1</v-icon>
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn small v-on:click="plus()">
              <v-icon>mdi-plus-one</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

  </v-container>
</template>

<script>
export default {
  name: 'Board',
  methods: {
    plus: function (title) {
      if (title === 'ATT') {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp,
          attack: this.scoreHistory[this.scoreNumber].attack += 1,
          voltage: this.scoreHistory[this.scoreNumber].voltage,
          defence: this.scoreHistory[this.scoreNumber].defence
        })
      } else if (title === 'VOL') {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp,
          attack: this.scoreHistory[this.scoreNumber].attack,
          voltage: this.scoreHistory[this.scoreNumber].voltage += 1,
          defence: this.scoreHistory[this.scoreNumber].defence
        })
      } else if (title === 'DEF') {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp,
          attack: this.scoreHistory[this.scoreNumber].attack,
          voltage: this.scoreHistory[this.scoreNumber].voltage,
          defence: this.scoreHistory[this.scoreNumber].defence += 1
        })
      } else {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp += 1,
          attack: this.scoreHistory[this.scoreNumber].attack,
          voltage: this.scoreHistory[this.scoreNumber].voltage,
          defence: this.scoreHistory[this.scoreNumber].defence
        })
      }
      this.scoreNumber += 1
    },
    minus: function (title) {
      if (title === 'ATT') {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp,
          attack: this.scoreHistory[this.scoreNumber].attack -= 1,
          voltage: this.scoreHistory[this.scoreNumber].voltage,
          defence: this.scoreHistory[this.scoreNumber].defence
        })
      } else if (title === 'VOL') {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp,
          attack: this.scoreHistory[this.scoreNumber].attack,
          voltage: this.scoreHistory[this.scoreNumber].voltage -= 1,
          defence: this.scoreHistory[this.scoreNumber].defence
        })
      } else if (title === 'DEF') {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp,
          attack: this.scoreHistory[this.scoreNumber].attack,
          voltage: this.scoreHistory[this.scoreNumber].voltage,
          defence: this.scoreHistory[this.scoreNumber].defence -= 1
        })
      } else {
        this.scoreHistory.push({
          hp: this.scoreHistory[this.scoreNumber].hp -= 1,
          attack: this.scoreHistory[this.scoreNumber].attack,
          voltage: this.scoreHistory[this.scoreNumber].voltage,
          defence: this.scoreHistory[this.scoreNumber].defence
        })
      }
      this.scoreNumber += 1
    }
  },

  data: () => ({
    scoreNumber: 0,
    scoreHistory: [
      {
        hp: 15,
        attack: 0,
        voltage: 0,
        defence: 0,
      }
    ],
    cards: [
      {
        title: 'ATT',
        flex: 4,
        color: '#EF5350'
      },
      {
        title: 'VOL',
        flex: 4,
        color: '#00695C'
      },
      {
        title: 'DEF',
        flex: 4,
        color: '#1565C0'
      },
    ],
  }),
}
</script>
