<template>
  <div>
      <div id='map' class='map'> </div>
  </div>
</template>

<script>
export default {
  name: 'Map',
  mounted(){
          
    window.mapboxgl.accessToken = "pk.eyJ1Ijoic291aGVpYnQiLCJhIjoiY2tseG5kcHVtM2JucTJubjFsaWFlY3hibSJ9.1dQ9g54oEZBvWAF0FQCDZQ";	
    
    var map = new window.mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/dark-v9',
        center: [50.84789, 4.35199], 
        zoom: 4
    });
    map.on('load', (() => {
        this.markers.forEach(function(marker) {
            var el = document.createElement('div');
            el.className = 'marker';
            new window.mapboxgl.Marker(el)
                .setLngLat([parseFloat(marker.latitude), parseFloat(marker.longitude)])
                .addTo(map);
        });
        
        this.markers.forEach((x) => {
            document.getElementById(x.name)
                .addEventListener('click', () => {
                    map.flyTo({
                        center: [parseFloat(x.latitude), parseFloat(x.longitude)],
                        zoom: 9
                    })
                ;}
            )
        })
           
    }).bind(this));
  },
  props: {
    markers: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.marker {
  background-image: url('./../assets/mapbox-icon.png');
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}
.map { 
    height: 500px;
    border: #f6e767 3px solid;
    border-radius: 7px;
}
</style>