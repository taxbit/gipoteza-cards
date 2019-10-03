<template>
  <div class="card">
    <div class="card__date">{{card.date}}</div>
    <div v-if="card.status" class="card__status">{{card.status}}</div>
    
    <div v-if="card.gipoteza==null">
      <div class="card__add-icon">+</div>
      <div class="card__helper">
        Добавить гипотезу с дедлайном в этот день
      </div>
    </div>

    <div v-else>
      {{card.gipoteza}}
    </div>
  {{card.steps[0]}}
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: ['card'],
    data() {
      return {

      }
    },
  }
</script>

<style lang="scss" scoped>
  .card {
    border: 1px solid #E1E1E1;
    box-sizing: border-box;
    box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.08);
    border-radius: 4px;
    width: 235.78px;
    height: 115px;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;

      &__date {
        width: 50px;
        height: 15px;
        background: #E1E1E1;
        color: white;
        position: absolute;
        left: 18px;
        top: 13px;
        font-family: Roboto;
        font-style: normal;
        font-weight: 300;
        font-size: 10px;
        line-height: 12px;
        text-align: center;
        letter-spacing: 0.01em;
      }

      &__status {
        position: absolute;
        right: 10px;
        top: 13px;
        font-style: normal;
        font-weight: 300;
        font-size: 9px;
        line-height: 11px;
        text-align: center;
        letter-spacing: 0.01em;
      }

      &__add-icon {
        width: 40px;
        height: 40px;
        color: #E1E1E1;
        border-radius: 50%;
        border: 1px solid #E1E1E1;
        font-size: 33px;
        font-style: thin;
      }

      &__helper {
        font-family: Roboto;
        font-style: normal;
        font-weight: 300;
        font-size: 13px;
        line-height: 15px;
        letter-spacing: 0.01em;
        width: 144px;
        color: #E1E1E1;
      }

      &:hover {
        background-color: #109CF1;
        box-shadow: 0px 14px 40px rgba(0, 0, 0, 0.2);
        cursor: pointer;
        border-color: #109CF1;

        .card__date {
          background-color: transparent;
          border: 1px solid #E1E1E1;
        }
      }
  }
</style>
