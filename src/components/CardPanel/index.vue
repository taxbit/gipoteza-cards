<template>
  <div>
    <div class="card__panel-background" v-if="showPanel" @click="$emit('close')"></div>

    <transition name="slide-fade">
      <div class="card__panel" v-if="showPanel">
          <button class="card__panel-close" @click="$emit('close')" >+</button>

          <div class="card__panel-gipoteza">
            <h2>Добавьте свою гипотезу</h2>
            <h4>Моя гипотеза</h4>
            <input type="text" v-model="gipoteza" placeholder="Если я..., то смогу...">
          </div>

          <div v-if="card.date" class="card__panel-ddl">
            <span>DDL</span>
            <datepicker
              :language="ru"
              :format="customFormatter"
              v-model="ddl">
            </datepicker>
          </div>


          <div class="card__panel-steps">
            <h2>Добавьте действия для гипотезы</h2>
            <transition-group name="steps" tag="div" class="card__panel-steps">
              <div v-for="step in steps" :key="step.id" class="card__panel-step">
                <input type="checkbox" v-model="step.cheked">
                <input type="text" v-model="step.descr"
                @keyup.once="addStep(step.id)">
              </div>
            </transition-group>
          </div>

          <button class="card__panel-save" @click="saveCard()" :disabled="!gipoteza">
            Создать гипотезу
          </button>

      </div>
    </transition>
  </div>
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
        ddl: null,
        ru: ru,
      }
    },
    watch: {
      card() {
        this.gipoteza = this.card.gipoteza
        this.steps = JSON.parse(JSON.stringify(this.card.steps))
        this.ddl = new Date(this.card.date)
      }
    },
    methods: {
      saveCard() {
        this.$emit('saveCard', {
            'id': this.card.id,
            'gipoteza': this.gipoteza,
            'steps': this.steps,
            'ddl': this.ddl,
          })
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

