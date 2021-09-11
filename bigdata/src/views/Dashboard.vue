<template>
  <h1>Dashboard</h1>
  <div>
    <MonthlyChart />
    <!--<ColorTable /> -->
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import MonthlyChart from '../components/chart/MonthlyChart.vue'
import ColorTable from '../components/table/ColorTable.vue'
import { MDBContainer } from 'mdb-vue-ui-kit'

@Options({
  components: {
    MonthlyChart,
    MDBContainer,
    ColorTable
  }
})
export default class Dashboard extends Vue {}
</script>
