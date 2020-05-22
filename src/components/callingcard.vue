 <template>
  <div id="callingcard">
    <canvas ref="map"></canvas>
  </div>
</template>

<script>
import { GeoCoordinates } from "@here/harp-geoutils";
// import { MapControls } from "@here/harp-map-controls";
import { MapView } from "@here/harp-mapview";
import {
  APIFormat,
  OmvDataSource,
  AuthenticationMethod
} from "@here/harp-omv-datasource";
// import { harp } from "@here/harp-mapview";
export default {
  name: "callingcard",
  props: {
    msg: String
  },
  data() {
    return {
      map: null,
      token: "AG27oF-HTRmZXFq5OcsKAQA",
      camera: null,
      renderer: null,
      mesh: null
    };
  },
  methods: {
    init: function() {}
  },
  mounted() {
    this.map = new MapView({
      canvas: this.$refs.map,
      theme:
        "https://unpkg.com/@here/harp-map-theme@latest/resources/berlin_tilezen_night_reduced.json"
    });

    // const controls = new MapControls(this.map);
    const omvDataSource = new OmvDataSource({
      baseUrl: "https://vector.hereapi.com/v2/vectortiles/base/mc",
      apiFormat: APIFormat.XYZOMV,
      styleSetName: "tilezen",
      authenticationCode: "_Ydg1pQchvc2E4TOT-DSBu0XAiRSASbHD9TMCK-stDk",
      authenticationMethod: {
        method: AuthenticationMethod.QueryString,
        name: "apikey"
      }
    });
    this.map.addDataSource(omvDataSource);
    this.map.setCameraGeolocationAndZoom(
      new GeoCoordinates(Number(this.lat), Number(this.lng)),
      12
    );
    this.init();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#callingcard {
  position: absolute;
  height: 60vh;
  width: 60vw;
  top: 20vh;
  left: 20vw;
}
#map {
  width: 100%;
  height: 100%;
}
</style>