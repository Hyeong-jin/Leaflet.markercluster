Leaflet.markercluster
=====================

인터렉티브 자바스크립트 라이브러리 [Leaflet](http://leafletjs.com)를 위한 아름다운 동적의 마커 클러스터링 기능을 제공합니다.

*Leaflet 0.7.0 이상의 버전이 필요합니다.*

Leaflet 0.5 를 위한 버전, [Download b128e950](https://github.com/Leaflet/Leaflet.markercluster/archive/b128e950d8f5d7da5b60bd0aa9a88f6d3dd17c98.zip)<br>
Leaflet 0.4 를 위한 버전, [Download the 0.2 release](https://github.com/Leaflet/Leaflet.markercluster/archive/0.2.zip)


## 플러그인 사용하기

Bower를 통한 설치: `bower install leaflet.markercluster`

사용법은 포함된 예제를 보십시오.

[realworld example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld.388.html) 처음 시작하기 좋습니다. 이것은 클러스터의 모든 기본기능을 사용합니다.

클러스터의 표현과 동작을 커스터마이징 하는 방법을 알아보려면, [custom example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-custom.html)을 확인하십시오. 

### 사용방법
마커를 추가하기 위한 새로운 MarkerClusterGroup을 생성하고, 지도에 추가하십시오.

```javascript
var markers = new L.MarkerClusterGroup();
markers.addLayer(new L.Marker(getRandomLatLng(map)));
... Add more layers ...
map.addLayer(markers);
```

### 기본사항
기본적으로 Clusterer는 멋진 몇가지 사항이 활성화 되어 있습니다.
* **showCoverageOnHover**: 클러스터에 마우스가 올라갔을때 포함된 마커들의 범위를 보여줍니다.
* **zoomToBoundsOnClick**: 클러스터를 클릭했을때 범위를 확대합니다.
* **spiderfyOnMaxZoom**: 최대로 확대한 상태에서 클러스터를 클릭했을 때, 마커들을 볼 수 있도록 나선형으로 마커를 배치합니다(spiderfy). 그래서 모든 마커들을 볼 수 있습니다.
* **removeOutsideVisibleBounds**: 성능을 위해서 뷰포트로부터 너무 먼 클러스터와 마커를 지도에서 지웁니다.

MarkerClusterGroup 생성시에 원한다면 이러한 것들을 비활성화 할수 있습니다. 
```javascript
var markers = new L.MarkerClusterGroup({ 
      spiderfyOnMaxZoom  : false, 
      showCoverageOnHover: false, 
      zoomToBoundsOnClick: false 
    });
```

### 클러스터 마커 커스터마이징
클러스터 마커의 Icon을 만들기 위해서 당신이 만든 함수를 MarkerClusterGroup에 옵션으로 제공할 수도 있습니다.
기본 구현은 10에서 100까지의 범위에서 색을 변경하지만, 좀더 고급의 사용을 위해서 커스터마이징이 필요할 수 있습니다.
이 방법을 사용하려면 .Default를 포함하지 마십시오.
MarkerCluster를 전달할 때, 아이콘을 표시하기 위해 getChildCount()나 getAllChildMarkers()를 사용할 수 있습니다.

```javascript
var markers = new L.MarkerClusterGroup({
	iconCreateFunction: function(cluster) {
		return new L.DivIcon({ html: '<b>' + cluster.getChildCount() + '</b>' });
	}
});
```
이 예제를 확인하십오.
Check out the [custom example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-custom.html) 

### 모든 옵션
기본으로 설정된 옵션 (boolean options):
* **showCoverageOnHover**: 클러스터에 마우스를 올렸을 때 마커들의 범위를 보여줍니다.
* **zoomToBoundsOnClick**: 클러스터를 클릭하였을 때 범위를 크게 보여줍니다.
* **spiderfyOnMaxZoom**: 최대로 확대한 상태에서 클러스터를 클릭하였을 때 마커들을 볼 수 있도록 나선형으로 마커를 배치합니다(spiderfy). 그래서 모든 마커들을 볼 수 있습니다.
* **removeOutsideVisibleBounds**: 성능을 위해서 뷰포트로부터 너무 먼 클러스터와 마커를 지도에서 지웁니다. 

다른 옵션들
* **animateAddingMarkers**: true로 설정하면 지도에 MarkerClusterGroup를 추가한 후에 개별 마커를 (MarkerClusterGroup에) 추가하는 것은 마커를 추가하고 움직여서 클러스터로 합칩니다. 대량의 마커를 추가할 때 보다 나은 성능을 위해서 기본 설정은 false입니다. addLayers는 지원하지 않고, 개별 마커를 가진 addLayers만 지원합니다.
* **disableClusteringAtZoom**: If set, at this zoom level and below markers will not be clustered. This defaults to disabled. [See Example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld-maxzoom.388.html)
* **maxClusterRadius**: 중앙 마커에서 부터 커버하는 클러스터의 최대 반경(in pixels). 기본값은 80 입니다. 작은 값이면 더 작은 클러스터를 만들것입니다. 또한 현재 지도의 줌을 받아서 최대 클러스터 반경을 pixcel로 반환하는 함수를 사용할 수도 있습니다.
* **polygonOptions**: 클러스터의 경계를 보여주기 위해 L.Polygon(points, options)를 만들때 전달하는 옵션
* **singleMarkerMode**: true로 설정하면, 같은 크기의 클러스터로 보이게 하기 위해 추가된 모든 마커들의 아이콘을 대체합니다.
* **spiderfyDistanceMultiplier**: 나선형으로 배치되는 마커들이 위치한 중심으로부터 떨어진 거리를 증가시키기 위해 1부터 증가시킵니다. 커다란 마커 아이콘을 사용할때 설정하며 기본값은 1입니다.
* **iconCreateFunction**: 클러스터 아이콘을 생성하는 함수 [See default as example](https://github.com/Leaflet/Leaflet.markercluster/blob/15ed12654acdc54a4521789c498e4603fe4bf781/src/MarkerClusterGroup.js#L542).


## 이벤트
click, mouseover, 등의 이벤트를 등록하면, 클러스터 안의 마커와 연관을 맺습니다. 
클러스터의 이벤트를 받기위해서는 'cluster' + 'eventIWant'의 형식의 이벤트명을 사용합니다. 예: 'clusterclick', 'clustermouseover'.

두 경우 각각의 이벤트 핸들러의 예는 아래와 같습니다.

```javascript
markers.on('click', function (a) {
	console.log('marker ' + a.layer);
});

markers.on('clusterclick', function (a) {
	console.log('cluster ' + a.layer.getAllChildMarkers().length);
});
```

## 메소드

### Getting the bounds of a cluster
When you recieve an event from a cluster you can query it for the bounds.
See [example/marker-clustering-convexhull.html](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-convexhull.html) for a working example.
```javascript
markers.on('clusterclick', function (a) {
	map.addLayer(new L.Polygon(a.layer.getConvexHull()));
});
```

### Zooming to the bounds of a cluster
When you recieve an event from a cluster you can zoom to its bounds in one easy step.
If all of the markers will appear at a higher zoom level, that zoom level is zoomed to instead.
See [marker-clustering-zoomtobounds.html](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-zoomtobounds.html) for a working example.
```javascript
markers.on('clusterclick', function (a) {
	a.layer.zoomToBounds();
});
```

### Getting the visible parent of a marker
If you have a marker in your MarkerClusterGroup and you want to get the visible parent of it (Either itself or a cluster it is contained in that is currently visible on the map).
This will return null if the marker and its parent clusters are not visible currently (they are not near the visible viewpoint)
```
var visibleOne = markerClusterGroup.getVisibleParent(myMarker);
console.log(visibleOne.getLatLng());
```

### Adding and removing Markers
addLayer, removeLayer and clearLayers are supported and they should work for most uses.

### Bulk adding and removing Markers
addLayers and removeLayers are bulk methods for adding and removing markers and should be favoured over the single versions when doing bulk addition/removal of markers. Each takes an array of markers

If you are removing a lot of markers it will almost definitely be better to call clearLayers then call addLayers to add the markers you don't want to remove back in. See [#59](https://github.com/Leaflet/Leaflet.markercluster/issues/59#issuecomment-9320628) for details.

### Other Methods
````
hasLayer(layer): Returns true if the given layer (marker) is in the MarkerClusterGroup
zoomToShowLayer(layer, callback): Zooms to show the given marker (spidifying if required), calls the callback when the marker is visible on the map
addLayers(layerArray): Adds the markers in the given array from the MarkerClusterGroup in an efficent bulk method.
removeLayers(layerArray): Removes the markers in the given array from the MarkerClusterGroup in an efficent bulk method.
````

## Handling LOTS of markers
The Clusterer can handle 10000 or even 50000 markers (in chrome). IE9 has some issues with 50000.
[realworld 10000 example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld.10000.html)
[realworld 50000 example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld.50000.html)
Performance optimizations could be done so these are handled more gracefully (Running the initial clustering over multiple JS calls rather than locking the browser for a long time)

### License

Leaflet.markercluster is free software, and may be redistributed under the MIT-LICENSE.

[![Build Status](https://travis-ci.org/Leaflet/Leaflet.markercluster.png?branch=master)](https://travis-ci.org/Leaflet/Leaflet.markercluster)
