<template>
  <div class="yes-justified-elements">
    <div v-for="row in rows" class="yes-justified-elements__row">
      <slot v-bind:row="row" />
    </div>
  </div>
</template>
<script>
export default {
  props: {
    items: {
      type: Array,
      default: () => []
    },
    maxRowRatio: {
      type: Number,
      default: 3
    },
    minRowRatio: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {}
  },
  computed: {
    rows() {
      // Split the items into rows
      let rowRatio = 0
      let row = 0
      const items = this.items.map(item => {
        item.ratio = item.width / item.height
        rowRatio = rowRatio + item.ratio
        item.rowRatio = rowRatio
        item.row = row
        if (rowRatio > this.maxRowRatio) {
          row++
          rowRatio = 0
        }
        return item
      })

      // Group the items by row
      let rows = items.reduce(
        (row, item) =>
          Object.assign(row, {
            [item.row]: (row[item.row] || []).concat(item)
          }),
        []
      )

      // Set the width per item and the ratio per row
      rows = rows.map(row => {
        let rowRatio = row[row.length - 1].rowRatio
        rowRatio = rowRatio < this.minRowRatio ? this.minRowRatio : rowRatio
        const rowItems = row.map(item => {
          item.style = {}
          item.style.width = (item.ratio / rowRatio) * 100 + '%'
          return item
        })
        return {
          rowRatio: rowRatio,
          style: {
            paddingBottom: 100 / rowRatio + '%'
          },
          items: rowItems
        }
      })

      return rows
    }
  },
  mounted() {},
  methods: {}
}
</script>
<style scoped lang="scss">
</style>
