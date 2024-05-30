# EE_NDVI  (Google Earth Engine based NDVI)


import ee

import geemap

ee.Authenticate()

ee.Initialize (project='ee-imranak32')

Map= geemap.Map()
Map

Map.setCenter (67.0897, 24.8957, 10)

point= ee.Geometry.Point(67.0897, 24.8957)

imagecol= ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED").filterBounds(point)

image = ee.Image(imagecol.filterDate('2020-01-01', '2020-12-31').sort('CLOUD_COVERAGE_ASSESSMENT').first())

ndvi=image.normalizedDifference(['B8','B4'])

vis= {
    "min": -1,
    "max": 1,
    "palette": ['blue','white','Green']

}

Map.addLayer(ndvi, vis)
Map

