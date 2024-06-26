# EE_NDVI  (Google Earth Engine based NDVI)


import ee

import geemap

ee.Authenticate()

ee.Initialize (project='ee-imran*********')#your GEE project ID


# Create a map
Map = geemap.Map()
Map.setCenter(67.0897, 24.8957, 10)

# Define a point
point = ee.Geometry.Point(67.0897, 24.8957)

# Filter the image collection by the point
imagecol = ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED").filterBounds(point)

# Filter the image collection by date and sort by cloud coverage
image = ee.Image(imagecol.filterDate('2020-01-01', '2020-12-31').sort('CLOUD_COVERAGE_ASSESSMENT').first())

# Calculate NDVI
ndvi = image.normalizedDifference(['B8', 'B4'])

# Define visualization parameters
vis = {"min": -1, "max": 1, "palette": ['blue', 'white', 'green']}

# Add the NDVI layer to the map
Map.addLayer(ndvi, vis)

# Display the map
Map
