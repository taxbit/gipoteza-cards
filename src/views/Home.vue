<template>
  <div class="home">
    <Card v-for="item in cardCount" :key="item"
      :number='item'
      :month='month'
      @click.native="showPanel = !showPanel"
    />
    {{showPanel}}
    <CardPanel
      :showPanel="showPanel"
      @close="hideCardPanel()"
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
      month: 'июня',
      showPanel: false,
    }
  },
  methods: {
    hideCardPanel() {
      this.showPanel = false
    }
  },
}
</script>

<style lang="scss" scoped>
  .home {
    display: flex;
    flex-wrap: wrap;
    margin: 0px auto;
    border: 1px solid black;
    width: 1349px;
    height: 730px;
    padding: 77px 142px 73px;
    justify-content: space-between;
    position: relative;
  }
</style>
