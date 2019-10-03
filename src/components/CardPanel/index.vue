<template>
  <transition name="slide-fade">
    <div class="card__panel" v-if="showPanel">
      <button class="card__panel-close" @click="$emit('close')" >X</button>
      <h1>Добавьте свою гипотезу</h1>
      <label for="gipotezaDescription">Моя гипотеза</label>
      <textarea v-model="gipoteza" cols="30" rows="1"></textarea>

      <div class="card__panel-ddl">
        <span>DDL</span>
        <datepicker
          :language="ru" 
          :format="customFormatter">
        </datepicker>
      </div>

      <div v-for="step in steps" :key="step.id">
        <input type="checkbox" v-model="step.cheked">
        <input type="text" v-model="step.descr" 
        @keyup.once="addStep(step.id)">
      </div>
      {{steps}}
      <button class="card__save" @click="saveCard()">
        Создать гипотезу
      </button>
    </div>
  </transition>
</template>

<script>
  import Datepicker from 'vuejs-datepicker';
  import {ru} from 'vuejs-datepicker/dist/locale'
  import moment from 'moment'

  export default {
    name: 'CardPanel',
    props: ['showPanel', 'card'],
    components: {
      Datepicker,
    },
    data() {
      return {
        gipoteza: '',
        steps: [],
        stepsCount: 1,
        ru: ru,
      }
    },
    watch: {
      card() {
        this.gipoteza = this.card.gipoteza
        this.steps = JSON.parse(JSON.stringify(this.card.steps)) 
      }
    },
    methods: {
      saveCard() {
        this.$emit('saveCard', { 
          id: this.card.id, 
          gipoteza: this.gipoteza,
          steps: this.steps
          })
        //this.gipoteza = ''
      },
      addStep(id) {
        this.steps.push({
            'id': ++id,
            'cheked': false,
            'descr': '',
        })
      },
      customFormatter(date) {
        moment.locale('ru')
        return moment(date).format('DD MMMM, YYYY');
      }
    },

  }
</script>

<style lang="scss" scoped>

.card__panel {
  position: absolute;
  top: 0;
  right: 0;
  width: 447px;
  height: 100%;
  background: #FFFFFF;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.25);
  &-close {
    background: transparent;
    border: none;
    cursor: pointer;
    position: absolute;
    top: 5px;
    right: 5px;
  }

  &-ddl {
    span {
      color: #323C47;
    }
  }
}
.slide-fade {
  &-enter-active {
    transition: all .3s ease;
  }
  &-leave-active {
    transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  &-enter, &-leave-to
  {
    transform: translateX(10px);
    opacity: 0;
  }
}
</style>
