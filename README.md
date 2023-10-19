# api_coordinates_scrape

This script is designed to work around an API endpoint limitation that allows querying of locations based on coordinates but returns only a maximum of 50 locations closest to the given input, regardless of how many are actually there. The objective of the script is to ensure comprehensive retrieval of all locations within a given mapped polygon, in this case representing the area of the continental US.

How It Works
Initial Point Generation: Start by generating evenly distributed points across the mapped polygon.

API Query: For each point, query the API to retrieve up to 50 locations.

Determining the Maximum Distance: With the retrieved locations, determine the distance to the furthest location. This gives an understanding of the reach of our current query point.

Constructing Sub-Polygons: Use this distance to draw a circle around the query point with a radius equal to the distance of the furthest location. This circle represents the area we can be certain we've fully queried. By subtracting this circle from our main polygon, we get sub-polygons that represent areas we haven't yet fully covered.

Increasing Resolution: For these remaining sub-polygons, increase the resolution (i.e., generate more tightly packed points) and repeat the process.

Iterate: Continue the process iteratively, querying the API for each new point, constructing new sub-polygons, and increasing the resolution until there are no more sub-polygons left to query.

Notes
The code was for one-time use and was developed over a short period. It might not be the most efficient or neatly organized but serves its purpose for this specific project.
