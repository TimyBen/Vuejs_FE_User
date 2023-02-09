<template>
    <v-btn class="item" v-for="(value, key) in listfilter" :key="key">{{value}}</v-btn>
</template>

<script>
export default {
  name: 'FilterDropDown',
  data () {
    return {
      filter: false,
      selected_filter: '',
      listfilter: {
        item1: 'Tất cả',
        item2: 'Tuần này',
        item3: 'Tuần trước',
        item4: '2 Tuần trước'
      }
    }
  },
  methods: {
    filter_show: function () {
    }
  }
//   components: { InfoModal }
}

</script>

<style>
.item {
    width: 100%;
    background: #FFFFFF;
    display: flex;
    padding: 12px 16px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
    font-family: 'SVN-Gilroy';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    display: flex;
    align-items: center;
    color: #1A1A1A;
}
</style>
