<template>
  <div class="home">
    <Card v-for="card in cards" :key="card.id"
      :card='card'
      @click.native="showCardPanel(card)"
    />
    {{showPanel}}
    <CardPanel
      :showPanel="showPanel"
      :card="cardInPanel"
      @close="hideCardPanel()"
      @saveCard="saveCard"
    />
  </div>
</template>

<script>
import { Card, CardPanel } from '@/components'

export default {
  name: 'home',
  components: {
    Card,
    CardPanel
  },
  data() {
    return {
      cardCount: 16,
      cards: [],
      month: 'июня',
      showPanel: false,
      cardInPanel: null,
    }
  },
  mounted () {
    //тут будет запрос к API загрузки карт
    for (let i = 0; i < this.cardCount; i++) {
      this.cards.push({
        'id':i,
        'date': `${i} ${this.month}`,
        'status':null, 
        'gipoteza':null,
        'steps':[{
            'id': 0,
            'cheked': false,
            'descr': '',
          }],
        })
    }
  },
  methods: {
    hideCardPanel() {
      this.showPanel = false
    },
    showCardPanel(card) {
      this.showPanel = true
      this.cardInPanel = card
    },
    saveCard(upData) {
      this.showPanel = false

      //тут будет запрос к API на сохранение кары по cardUpdated.id
      let tempCard = this.cards.find(card => card.id===upData.id)
      tempCard.gipoteza = upData.gipoteza
      tempCard.steps = upData.steps

    }
  },
}
</script>

<style lang="scss" scoped>
  .home {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    align-items: center;
    justify-items: center;
    margin: 0px auto;
    width: 1349px;
    height: 730px;
    justify-content: space-between;
    position: relative;
  }
</style>
