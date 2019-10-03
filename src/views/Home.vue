<template>
  <div class="home">
    <Card v-for="card in cards" :key="card.id"
      :card='card'
      @click.native="showCardPanel(card)"
    />
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
import moment from 'moment'
import 'roboto-fontface/css/roboto/roboto-fontface.css'

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
        'date': this.getDate(i),
        'ddl' : this.getDate(i),
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
      this.cards.forEach(card => {
        if (card.id===upData.id) {
          card.gipoteza = upData.gipoteza
          card.steps = upData.steps
          card.ddl = upData.ddl
          card.status = moment(upData.ddl) < moment() ? 'Просрочена' : 'Ожидает теста'
        }
      })

    },
    getDate(add) {
      moment.locale('ru')
      return moment().startOf('month').add(add, 'days');
    }

  },
}
</script>

