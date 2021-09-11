<template>
  <h1>Dashboard</h1>
  <div>
    <kakaoMap />
    <!--<ColorTable /> -->
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import MonthlyChart from '../components/chart/MonthlyChart.vue'
import ColorTable from '../components/table/ColorTable.vue'
import { MDBContainer } from 'mdb-vue-ui-kit'
import KakaoMap from '../components/map/KakaoMap.vue'

@Options({
  components: {
    MonthlyChart,
    MDBContainer,
    ColorTable,
    KakaoMap
  }
})
export default class Dashboard extends Vue {}
</script>
