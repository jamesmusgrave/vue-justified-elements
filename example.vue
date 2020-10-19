<template>
  <div>
    <input v-model="maxRowRatio" type="range" min="1" max="10">
    <yes-justified-elements
      :items="items"
      :maxRowRatio="maxRowRatio"
      :minRowRatio="maxRowRatio*.7"
    >
      <template v-slot:default="{row}">
        <div :style="row.style" class="row">
          <div class="row__list">
            <div v-for="item in row.items" :style="item.style" class="row__list__item">
              {{ row.rowRatio }}<br>{{ row.style.paddingBottom }}<br>{{ item.ratio }}<br>{{ item.style.width }}
            </div>
          </div>
        </div>
      </template>
    </yes-justified-elements>
  </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  components: {},
  data() {
    return {
      maxRowRatio: 1,
      items: [
        {
          width: 500,
          height: 300
        },
        {
          width: 300,
          height: 800
        },
        {
          width: 800,
          height: 500
        },
        {
          width: 400,
          height: 200
        },
        {
          width: 600,
          height: 500
        },
        {
          width: 400,
          height: 500
        },
        {
          width: 200,
          height: 300
        },
        {
          width: 700,
          height: 500
        },
        {
          width: 400,
          height: 600
        }
      ]
    }
  }
}
</script>
<style lang="scss">
.row {
  position: relative;
}
.row__list {
  position: absolute;
  display: flex;
  height: 100%;
  width: 100%;
  justify-content: center;
}
.row__list__item {
  height: 100%;
  border: 1px solid red;
}
</style>
