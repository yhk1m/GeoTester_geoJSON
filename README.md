# 지오테스터 한국 경계 자료 (GeoTester_geoJSON)

[지오테스터(GeoTester)](https://geotester.bgnl.kr)가 한반도 지도를 그릴 때 쓰는 대한민국 행정구역 경계 GeoJSON 모음입니다. 법정구역 SHP 파일을 GeoJSON으로 바꾼 것이며, 시도, 시군구, 구 단위와 남한 해안선 윤곽이 들어 있습니다. 좌표는 경위도가 아니라 미터 단위 투영 좌표(EPSG:5179, UTM-K)입니다.

## 파일

| 파일 | 도형 수 | 내용 | 속성 |
|---|---|---|---|
| `geoJsonData_korea_sido.geojson` | 17 | 시도 경계 (광주와 전남이 따로 있는 17개 시도) | `CTPRVN_CD`, `CTP_KOR_NM` |
| `geoJsonData_korea_sigungu.geojson` | 160 | 도의 시와 군, 특별시와 광역시는 통째로 하나 | `SIG_CD`, `SIG_KOR_NM`, `CTP_KOR_NM` |
| `geoJsonData_korea_SIG.geojson` | 112 | 특별시, 광역시의 자치구와 일반시의 구 | `SIG_CD`, `SIG_KOR_NM`, `CTP_KOR_NM` |
| `koreaSidoGeoJsonMerged.geojson` | 16 | 더 자세한 시도 경계. 광주와 전남이 `전남광주통합특별시` 하나로 합쳐져 있음 | `CTPRVN_CD`, `CTP_KOR_NM` |
| `koreaSouthMerged.geojson` | 1 | 시도 경계 없이 남한 바깥 윤곽만 남긴 상세 해안선 | `FID` |

`geoJsonData_korea_sigungu.geojson`에서는 서울, 부산 같은 특별시와 광역시가 도형 하나입니다. 자치구까지 나누어 그리려면 `geoJsonData_korea_SIG.geojson`을 함께 씁니다.

## 좌표계 주의

다섯 파일 모두 좌표가 EPSG:5179(UTM-K, 미터 단위)입니다. 시도, 시군구 파일 머리에는 `CRS84`(경위도)라고 적혀 있지만 실제 값은 `954491, 1959777`처럼 미터 단위이므로, 웹 지도(Leaflet 등)에 올리기 전에 경위도로 바꿔야 합니다. 지오테스터는 [proj4](https://github.com/proj4js/proj4js)로 아래 정의를 써서 바꿉니다.

```
+proj=tmerc +lat_0=38 +lon_0=127.5 +k=0.9996 +x_0=1000000 +y_0=2000000 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs
```

## 지오테스터에서 쓰는 법

지오테스터는 학교망에서 외부 주소가 막히는 일이 있어, 이 저장소의 파일을 직접 불러오지 않고 받아서 자기 사이트의 `public/geojson/`에 넣어 둡니다.

| 이 저장소 | 지오테스터 |
|---|---|
| `geoJsonData_korea_sido.geojson` | `korea_sido.json` |
| `geoJsonData_korea_sigungu.geojson` | `korea_sigungu.json` |
| `geoJsonData_korea_SIG.geojson` | `korea_sig.json` |
| `koreaSouthMerged.geojson` | `korea_south_coastline.json` (지도를 PNG로 저장할 때만 받음) |

`koreaSidoGeoJsonMerged.geojson`은 광주와 전남이 합쳐져 있어 지오테스터에서는 쓰지 않습니다.

## 자료 출처

원본 SHP 파일과 GeoJSON 변환 방법은 아래 글을 따랐습니다.

- http://www.gisdeveloper.co.kr/?p=2332
- https://jgws.tistory.com/entry/대한민국-법정구역-SHP-파일을-GeoJSON으로-변환하기

## 만든 사람

양정고등학교 지리교사 김용현  
문의: bgnlkim@gmail.com
