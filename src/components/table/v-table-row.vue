<template>
  <div class="v-table-row">
    <div class="row row__first_name">{{row__data.first_name}}</div>
    <div class="row row__last_name">{{row__data.last_name}}</div>
    <div class="row row__id">{{row__data.id}}</div>
    <div class="row row__email">{{row__data.email}}</div>
  </div>
</template>


<script>
export default {
  name: "v-table-row",
  props: {
    row__data: {
      type: Object,
      default: () => {
        return {}
      }
    }
  },
  data() {
    return {
      
    }
  },
  computed: {}
}
</script>

<style>
  .v-table-row {
    display: flex;
    justify-content: space-around;
  }
  .row {
    flex-basis: 25%;
    padding: 8px 0px;
    text-align: left;
  }
</style>