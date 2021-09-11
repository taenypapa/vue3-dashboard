<template>
  <div id="map" style="width:100%;height:700px;"></div>
</template>
<script>
import { defineComponent, createApp } from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import KakaoMap from './KakaoMap.vue'

const app = createApp(KakaoMap)
app.use(VueAxios, axios)

export default defineComponent({
  name: 'KakaoMap',
  data () {
    return {
      markers: []
    }
  },
  mounted () {
    this.getMarkers()
    window.kakao && window.kakao.maps ? this.initMap() : this.addScript()
  },
  methods: {
    initMap () {
      var mapContainer = document.getElementById('map')
      var mapOption = {
        center: new kakao.maps.LatLng(36.450701, 127.570667), // 지도의 중심좌표
        level: 13 // 지도의 확대 레벨
      }

      var map = new kakao.maps.Map(mapContainer, mapOption) // 지도를 생성합니다

      var positions = []

      console.log(this.markers)
      this.markers.forEach((item) => {
        positions.push({
          title: item.name,
          latlng: new kakao.maps.LatLng(item.lat, item.lng)
        })
      })

      // 마커 이미지의 이미지 주소입니다
      var imageSrc = 'https://t1.daumcdn.net/localimg/localimages/07/mapapidoc/markerStar.png'

      for (var i = 0; i < positions.length; i++) {
        // 마커 이미지의 이미지 크기 입니다
        var imageSize = new kakao.maps.Size(24, 35)

        // 마커 이미지를 생성합니다
        var markerImage = new kakao.maps.MarkerImage(imageSrc, imageSize)

        // 마커를 생성합니다
        var marker = new kakao.maps.Marker({
          map: map, // 마커를 표시할 지도
          position: positions[i].latlng, // 마커를 표시할 위치
          title: positions[i].title, // 마커의 타이틀, 마커에 마우스를 올리면 타이틀이 표시됩니다
          image: markerImage // 마커 이미지
        })
      }
    },
    addScript () {
      const script = document.createElement('script') /* global kakao */
      script.onload = () => kakao.maps.load(this.initMap)
      script.src = 'http://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=19ecf43dc6b35f47a65701eefdbd9bd3'
      document.head.appendChild(script)
    },
    async getMarkers () {
      await axios.get('http://localhost:8081/v1/center').then((response) => {
        response.data.forEach(element => {
          this.markers.push({
            name: element.name,
            lat: element.lat,
            lng: element.lng
          })
        })
      })
    }
  }
})
</script>
