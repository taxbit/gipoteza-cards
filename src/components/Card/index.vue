<template>
  <div class="card" :class="{card_active : card.gipoteza}">

    <div class="card__date">{{customFormatter(card.date)}}</div>

    <div v-if="card.status" class="card__status"
      :class="{card__status_out:timeout}">
      {{card.status}}
    </div>

    <div class="card__add" v-if="card.gipoteza==null">
      <div class="card__add-icon">+</div>
      <div class="card__add-helper">
        Добавить гипотезу <span>с дедлайном в этот день</span>
      </div>
    </div>

    <div class="card__gipoteza" v-else>
      {{card.gipoteza}}
    </div>

  </div>
</template>

<script>
  import moment from 'moment'

  export default {
    name: 'Card',
    props: ['card'],
    data() {
      return {
      }
    },
    computed: {
      timeout() {
        return this.card.status == "Просрочена"
      }
    },
    methods: {
      customFormatter(date) {
        moment.locale('ru')
        return moment(date).format('D MMMM');
      }
    },
  }
</script>

