# Project Documentation: Security Incident Analysis with Power BI Dashboard and QGIS Map Visualization
## Project Overview

This project aims to analyze security incidents involving humanitarian aid workers, delivering actionable insights into incident patterns, victim demographics, and organizational involvement. Leveraging advanced data modeling, geospatial analysis, and interactive dashboards, the project empowers security managers and analysts in the humanitarian sector to make informed strategic and operational decisions. The products involve a Power BI dashboard with 2 pages and a QGIS map visualization (pdf). 

<img align="left" width="461" height="259"  alt="Aid workers security incidents dashboard" style="margin: 0 10px 0 0;" src="Images/Aid workers security incidents global overview.png"/> 
  
<img align="left" width="461" height="259"  alt="Aid workers security incidents dashboard" style="margin: 0 10px 0 0;" src="Images/Aid workers security incidents EM view.png"/> 
<br clear="left"/>
<small style="color:gray; font-size: 0.8em;"><em>Screenshots: Power BI dashboard pages: global overview and region view</em></small>
<br clear="left"/>

### Interactive Pages in Power BI Dashboard:
1.	Global Overview (1997–2024): Visualizes global trends using heatmaps and aggregated victim counts.
2.	East Mediterranean Humanitarian Corridor (2012–2024): Delivers detailed insights into provincial-level incidents using custom maps.

### Data Sources:

**Primary Dataset:**
_security_incidents_2024-11-22.csv_ contains detailed records of security incidents, including victim counts and organizational affiliations. The data is sourced from Humanitarian Outcomes' Aid Worker Security Database (aidworkersecurity.org).

**Geographic Data:**
Shapefiles for Israel, Palestine, Lebanon, and Syria were downloaded from GADM, standardized, merged, and converted into the TopoJSON format for Power BI integration.

### DAX Measures:
-	Victim Count: Total victims by type.
-	Incident Count: Total incidents by type.
-	Dynamic Map Title: Adapts titles based on slicer selections.

---

## 2. Data Model

### Primary Table:
Name: security_incidents_2024-11-22
Key Columns:
-	Incident ID
-	Date Fields (Year, Month, Day)
-	Victim Counts (e.g., Killed, Wounded, Kidnapped) by Organizational Affiliation and Gender
-	Means of Attack, Attack Context, and Location
-	Geographic Details (Country, Region/Province, City)
-	Latitude/Longitude
-	Details Text for incident descriptions

### Dimension Tables:

#### Organization: 
- Lists unique organization names for filtering incidents by humanitarian agencies and actors.
#### Type Casualty: 
- Represents casualty types (Killed, Wounded, Kidnapped) for cross-filtering.
#### Bridge Table:
- Links the primary table to dimension tables using composite keys (Incident ID, Organization ID, and Casualty ID). Enables accurate cross-filtering.
#### Calendar Table:
- Supports temporal analysis with calculated fields for Year, Month, and Week Number.

---

## 3. Maps

### Power BI Maps for Global and Reginal Analyses
-	Utilizes Power BI's Bing Maps for global and regional analysis and a custom shape map created for specific insights within the East Mediterranean Humanitarian Corridor.
-	Bubble maps visualize incidents based on latitude and longitude, with bubble size and color representing victim counts. The shape map for the East Mediterranean area is also colored by victim counts.

### QGIS Map Visualisation for Regional Analysis
-	Utilizes the shape map for both country and provincial-level insights within the East Mediterranean Humanitarian Corridor.
-	Data points in the shape map are locations identified by latitude and longitude, with symbols representing attack types.

<img align="left" width="600" height="424"  alt="Aid workers security incidents dashboard" style="margin: 0 10px 0 0;" src="Images/QGIS Map-East Mediterranean Humanitarian Corridor.png"/> 
<br clear="left"/>
<small style="color:gray; font-size: 0.8em;"><em>Screenshot: QGIS Map visualization</em></small>
<br clear="left"/>

### Creation Process:
1.	Standardized shapefiles for individual countries using QGIS. 
2. Merged shapefiles into a single dataset. 
3. Converted the merged shapefile to TopoJSON format using MapShaper for the Power BI dashboard.
4. Standardized province names to ensure alignment with incident data.
5.	Merged the final shapefile with the incidents dataset using QGIS.
6.	Created symbols to represent data points and adjusted the map for the print layout in QGIS.

### Challenges:
-	Name Standardization: Manual adjustments were required to address inconsistencies (e.g., 'Ar-Raqqah' vs. 'Ar Raqqah'), ensuring accurate matching with the dataset.
-	Projection Compatibility: Re-projected shapefiles to EPSG:4326 (WGS 84) for consistent integration.

---

## 4. Key Power BI Measures

### Victim Count:
- Calculates total victims (Killed, Wounded, Kidnapped) based on slicer selections for Organization and Casualty Type.
Full DAX logic is provided in the appendix.

### Incident Count:
Following the same DAX logic, counts distinct incidents filtered by Organization and Casualty Type slicers.

---

## 5. Relationships and Cross-Filtering in the Dashboard

### Bridge Table Role:
Addresses many-to-many relationships between organizations and casualty types, allowing mutual cross-filtering across dimension tables.

<img align="left" width="400" height="300"  alt="Inventory Dashboard" style="margin: 0 10px 0 0;" src="Images/Data model.png"/>
<br clear="left"/>
<small style="color:gray; font-size: 0.8em;"><em>Screenshot: Data model illustration</em></small> 

### Configuration:

#### Relationships:
   - Bridge Table → Organization (Many-to-One)
   - Bridge Table → Type Casualty (Many-to-One)
   -	Bridge Table ↔ Primary Table (Both Directions)

 #### Filter Direction:
   - Single-direction filters for dimension tables; bidirectional filters between the Bridge Table and Primary Table for seamless slicer functionality.
 <br clear="left"/>

---

## 6. Assumptions & Limitations

### Assumptions:
1.	Incident IDs in the primary table are unique.
2.	Missing values (e.g., blank dates, missing Region/Province names) were addressed using reverse geocoding (Python) and manual adjustments in Power Query.
   
### Limitations:
1.	Performance: Complex measures may reduce responsiveness with larger datasets.
2.	Geographic Completeness: Some province-level data relies on approximate latitude/longitude or manual corrections.

---

## 7. Future Enhancements for the Dashboard

### Performance Optimization:
Streamline DAX measures and SWITCH statements.
### Additional Filters:
Add filters for Actor Type, Actor Name, and Actor Motive.

---

## 8. Conclusion
The products of this project—Power BI dashboard and QGIS map visualization—deliver actionable insights into security risks, enabling humanitarian organizations to enhance resource allocation, risk assessment, and policy development. By integrating data cleaning, modeling, and geospatial tools, the project highlights the potential of advanced data analysis and GIS in addressing complex humanitarian challenges. It serves as a scalable blueprint for future analyses and a practical guide for analysts aiming to leverage advanced data and GIS techniques for impactful decision-making and reporting.

---

## 9. Appendix
-	M code for handling missing data, name standardization, and auxiliary table joins
- DAX code for dynamic measures and visualization titles
- Python code for reverse geocoding
- Aid worker security database codebook, published by Humanitarian Outcomes in 2021


_Note: The data points indicating incident locations are approximate rather than exact, due to the imputation of missing values in the latitude and longitude columns._
