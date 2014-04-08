Leaflet.markercluster
=====================

인터렉티브 자바스크립트 라이브러리 [Leaflet](http://leafletjs.com)를 위한 아름다운 동적의 마커 클러스터링 기능을 제공합니다.

*Leaflet 0.7.0 이상의 버전이 필요합니다.*

Leaflet 0.5 를 위한 버전, [Download b128e950](https://github.com/Leaflet/Leaflet.markercluster/archive/b128e950d8f5d7da5b60bd0aa9a88f6d3dd17c98.zip)<br>
Leaflet 0.4 를 위한 버전, [Download the 0.2 release](https://github.com/Leaflet/Leaflet.markercluster/archive/0.2.zip)


## 플러그인 사용하기

Bower를 통한 설치: `bower install leaflet.markercluster`

사용법은 포함된 예제를 보십시오.

[realworld example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld.388.html) 처음 시작하기에 좋습니다. 이것은 클러스터의 모든 기본기능을 사용합니다.

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
이에 대한 [예제](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-custom.html)를 확인하십오 

### 모든 옵션
기본 옵션 (boolean options):
* **showCoverageOnHover**: 클러스터에 마우스를 올렸을 때 마커들의 범위를 보여줍니다.
* **zoomToBoundsOnClick**: 클러스터를 클릭하였을 때 범위를 크게 보여줍니다.
* **spiderfyOnMaxZoom**: 최대로 확대한 상태에서 클러스터를 클릭하였을 때 마커들을 볼 수 있도록 나선형으로 마커를 배치합니다(spiderfy). 그래서 모든 마커들을 볼 수 있습니다.
* **removeOutsideVisibleBounds**: 성능을 위해서 뷰포트로부터 너무 먼 클러스터와 마커를 지도에서 지웁니다. 

다른 옵션
* **animateAddingMarkers**: true로 설정하면 지도에 MarkerClusterGroup를 추가한 후에 개별 마커를 (MarkerClusterGroup에) 추가하는 것은 마커를 추가하고 움직여서 클러스터로 합칩니다. 대량의 마커를 추가할 때 보다 나은 성능을 위해서 기본 설정은 false입니다. addLayers는 지원하지 않고, 개별 마커를 가진 addLayers만 지원합니다.
* **disableClusteringAtZoom**: If set, at this zoom level and below markers will not be clustered. This defaults to disabled. [예제](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld-maxzoom.388.html)
* **maxClusterRadius**: 중앙 마커에서 부터 커버하는 클러스터의 최대 반경(in pixels). 기본값은 80 입니다. 작은 값이면 더 작은 클러스터를 만들것입니다. 또한 현재 지도의 줌을 받아서 최대 클러스터 반경을 pixcel로 반환하는 함수를 사용할 수도 있습니다.
* **polygonOptions**: 클러스터의 경계를 보여주기 위해 L.Polygon(points, options)를 만들때 전달하는 옵션
* **singleMarkerMode**: true로 설정하면, 같은 크기의 클러스터로 보이게 하기 위해 추가된 모든 마커들의 아이콘을 대체합니다.
* **spiderfyDistanceMultiplier**: 나선형으로 배치되는 마커들이 위치한 중심으로부터 떨어진 거리를 증가시키기 위해 1부터 증가시킵니다. 커다란 마커 아이콘을 사용할때 설정하며 기본값은 1입니다.
* **iconCreateFunction**: 클러스터 아이콘을 생성하는 함수 [기본예제](https://github.com/Leaflet/Leaflet.markercluster/blob/15ed12654acdc54a4521789c498e4603fe4bf781/src/MarkerClusterGroup.js#L542).


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

### 클러스터의 경계 얻기
클러스터로부터 이벤트를 얻을 때, 경계를 조회할 수 있습니다.
예제로 [example/marker-clustering-convexhull.html](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-convexhull.html)를 보십시오.
```javascript
markers.on('clusterclick', function (a) {
	map.addLayer(new L.Polygon(a.layer.getConvexHull()));
});
```

### 클러스터의 경계에 맞추어 확대
클러스터로부터 이벤트를 받을때, 간단하게 경계에 맞게 확대할 수 있습니다.
높은 줌 레벨에서 모든 마커를 볼 수 있을 때, 현재의 줌에서 높은 레벨의 줌으로 확대 됩니다.
예제로 [marker-clustering-zoomtobounds.html](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-zoomtobounds.html)을 보십시오.
```javascript
markers.on('clusterclick', function (a) {
	a.layer.zoomToBounds();
});
```

### 마커의 보이는 부모(마커 자체나 마커를 포함한 클러스터)를 얻기
MarkerClusterGroup에 마커가 있고 보이는 부모를 얻고 싶을때 사용합니다. (마커나 그것을 포함한 클러스터가 지도 상에서 현재 보일때).
마커와 그것을 포함한 클러스터가 현재 보이지 않는다면 null을 반환합니다(볼 수 있는 뷰포트에 근접해 있지 않습니다).

```javascript
var visibleOne = markerClusterGroup.getVisibleParent(myMarker);
console.log(visibleOne.getLatLng());
```

### 마커 추가 및 삭제하기
addLayer, removeLayer 그리고 clearLayers 를 사용할 수 있고 대부분의 용도로 작동합니다.

### 대량의 마커를 추가 및 삭제하기
addLayers와 removeLayers는 대량으로 마커를 추가 삭제하기 위한 메소드입니다. 마커를 대량으로 추가/삭제시 단일 버전 보다 선호됩니다. 각각은 마커의 배열을 받습니다.

많은 양의 마커를 삭제하려면 거의 확실히 clearLayers를 호출하고 addLayers를 호출하여 삭제를 원하지 않는 마커를 다시 추가하는 것이 좋습니다. 상세한 것은 [#59](https://github.com/Leaflet/Leaflet.markercluster/issues/59#issuecomment-9320628)를 보십시오.


### 다른 메소드
````
hasLayer(layer): 주어진 layer(marker)가 MarkerClusterGroup안에 있다면 true를 반환
zoomToShowLayer(layer, callback): 주어진 마커를 (필요하면 클러스터를 나선형(spidifying)으로 풀어서) 보여주고 확대합니다. 지도상에 마커가 보여질때 callback을 호출합니다.
addLayers(layerArray): 효율적인 대량의 방법으로 MarkerClusterGroup에서 주어진 배열의 마커들을 추가합니다.
removeLayers(layerArray): 효율적인 대량의 방법으로 MarkerClusterGroup에서 주어진 배열의 마커들을 삭제합니다.
````

## 많은 양의 마커 처리
(크롬에서) Clusterer는 마커를 10000개나 50000개 까지도 처리할 수 있습니다. IE9는 50000개에서 문제가 발생합니다.
[realworld 10000 example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld.10000.html)
[realworld 50000 example](http://leaflet.github.com/Leaflet.markercluster/example/marker-clustering-realworld.50000.html)
성능 최적화를 통해 더 적절하게 처리됩니다(긴 시간동안 브라우저를 사용하지 못하게 하지 않고 여러 JS 호출을 통해 클러스터링 초기화를 실행합니다).

### License

Leaflet.markercluster is free software, and may be redistributed under the MIT-LICENSE.

[![Build Status](https://travis-ci.org/Leaflet/Leaflet.markercluster.png?branch=master)](https://travis-ci.org/Leaflet/Leaflet.markercluster)
