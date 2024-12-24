# TD3: Spatial SQL Functions

This guide explores advanced spatial SQL functions for analyzing and manipulating spatial data in PostGIS. By the end of this tutorial, you will learn how to perform spatial queries such as proximity analysis and area calculations.

## Prerequisites

- A PostgreSQL database with PostGIS installed and configured (refer to TD1 if needed).
- Spatial tables with relevant geometry data (refer to TD2 for creating spatial tables).

## Objectives

1. Count the number of parcels within a 1 km radius of specific fire points.
2. Calculate the total area of parcels near the fire points.

## Steps to Follow

### 1. Download and Import the Parcels Shapefile

1. **Download the Shapefile**:
   - Use the following [link](https://maps.leegov.com/datasets/80708a2f5f56426f94c8be97c182176b/about) to download the parcels shapefile.

2. **Import the Shapefile into PostGIS**:
   - Open the **PostGIS Shapefile Import/Export Manager**:
     - On Windows, search for "Shapefile Import" in the Start menu.
   - Select the downloaded shapefile.
   - Specify the target database and schema.
   - Click `Import` to load the shapefile into your database.
   - Verify that the parcels table has been created in your database.

### 2. Count Parcels within 1 km Radius

Use the following SQL query to count the parcels within 1 km of the specified fire points:

```sql
SELECT count(*)
FROM "public"."parcels"
WHERE ST_DWithin(
    geom, 
    (SELECT ST_Centroid(geom) FROM "public"."parcels" WHERE gid = 462273), 
    1000
) OR ST_DWithin(
    geom, 
    (SELECT ST_Centroid(geom) FROM "public"."parcels" WHERE gid = 460957), 
    1000
);
```

- This query uses `ST_DWithin` to find parcels within 1 km of two fire points.
- The fire points are calculated as centroids of the parcels with `gid = 462273` and `gid = 460957`.

#### Result:
The result of the query shows **472 parcels** within the specified radius.

### 3. Calculate Total Area of Parcels

To calculate the total area of the parcels within the same radius, use the following query:

```sql
SELECT SUM(shape_area)
FROM "public"."parcels"
WHERE ST_DWithin(
    geom, 
    (SELECT ST_Centroid(geom) FROM "public"."parcels" WHERE gid = 462273), 
    1000
) OR ST_DWithin(
    geom, 
    (SELECT ST_Centroid(geom) FROM "public"."parcels" WHERE gid = 460957), 
    1000
);
```

- `shape_area` is used to sum up the area of the parcels.

#### Result:
The total area of the parcels within the 1 km radius is **5,192,474.35 square units**.

## Additional Notes

1. **Visualization in QGIS**:
   - Duplicate the parcel layer and apply a filter using the same `ST_DWithin` logic.
   - Change the symbology to highlight the parcels within the risk zones.

2. **Expanding Analysis**:
   - Add more fire points or adjust the radius to refine the analysis.
   - Use functions like `ST_Intersection` to calculate overlapping areas.

## Resources

- [PostGIS Documentation](https://postgis.net/documentation/)
- [QGIS Documentation](https://qgis.org/en/docs/)

Feel free to experiment with different spatial queries to deepen your understanding!