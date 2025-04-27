# Mapping and Analyzing Security Incidents to Enhance the Safety of Humanitarian Aid Workers in High-Risk Areas
## 1. Project Overview
This project enhances the safety of humanitarian aid workers by analyzing security incidents where they were killed, wounded, or kidnapped from 1997 to 2024. Deliverables include:

- A three-page interactive **[Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZGFhYWZiZTMtM2FmMi00OTM3LWIzNGQtNGRhODQxMzc3NjZiIiwidCI6IjVlNmFlYmFjLWQ1OGItNGIwYi1iMmE2LTY1YTdjYWMxMGM0NSIsImMiOjl9)** hosted on Power BI Server.
- A complementary QGIS map visualization (PNG).

These tools provide actionable insights into incident patterns, victim demographics, organizational involvement, and geographic hotspots. By integrating advanced data modeling, geospatial analysis, and dynamic visualizations, the project empowers security managers and humanitarian organizations to make informed strategic and operational decisions in high-risk areas.

Interactive Dashboard Pages:

- Global Overview (1997–2024): Displays global trends with heatmaps and aggregated victim counts.
- East Mediterranean Humanitarian Corridor (2012–2024): Offers detailed insights into provincial-level incidents using custom maps.
- East Mediterranean Humanitarian Corridor - 2024: Visualizes means of attack and locations using the icon-map plugin.

![Global Dashboard Overview](Images/Aid%20workers%20security%20incidents%20global%20overview.png)

*Figure 1: Power BI Dashboard Global View.*

## 2. Data Sources
Incident Data:
The primary dataset, security_incidents_2024-11-22.csv, contains detailed records sourced from the Aid Worker Security Database by Humanitarian Outcomes. Fields include victim counts, organizational affiliations, attack contexts, and geographic details.

Geographic Data:
Shapefiles for Israel, Palestine, Lebanon, and Syria were sourced from GADM (gadm.org), standardized, and merged. These shapefiles were converted to TopoJSON and GeoJSON formats for seamless integration with Power BI.

## 3. Data Model
### Primary Table
Name: security_incidents_2024-11-22
Key Columns:

- Incident ID
- Date (Year, Month, Day)
- Victim Counts by Type, Organizational Affiliation, and Gender
- Means of Attack, Context, and Location
- Geographic Details (Country, Region, City, Latitude/Longitude)
- Incident Descriptions

### Dimension Tables
- Organization: Enables filtering by humanitarian agencies.
- Type Casualty: Filters incidents by casualty types (Killed, Wounded, Kidnapped).
- Bridge Table: Resolves many-to-many relationships between primary and dimension tables.
- Calendar Table: Supports temporal analysis with fields for Year, Month, and Week.

## 4. Maps
### Power BI Maps
#### Azure/Bing Map
- Azure Map: Serves as a heatmap to visualize the concentration of victim counts in geographic locations based on latitude and longitude information.
- Bing Map: Used as an alternative for public sharing of the dashboard via Power BI server, ensuring accessibility and compliance with licensing requirements.
#### Shape Map
- Highlights areas with higher victim counts, enabling interactive filtering between visuals. This visualization is particularly effective for identifying regional patterns and trends.

![East Mediterranean Dashboard](Images/Aid%20workers%20security%20incidents%20EM%20view.png)

*Figure 2: Power BI Dashboard East Mediterranean Humanitarian Corridor View with Shape Map.*

#### Icon-Map Plugin
- Combines interactivity with a first-glance overview of attack types. Customized icons represent different means of attack and their geographic distribution, providing actionable insights for operational planning.

![East Mediterranean Dashboard-IconMap](Images/Aid%20workers%20security%20incidents%20EM%202024%20icon%20map.png)

*Figure 3: Power BI Dashboard East Mediterranean Humanitarian Corridor 2024 with Icon Map.*

### QGIS and Data Preparation
QGIS was used to preprocess and standardize geographic data for the East Mediterranean Humanitarian Corridor. The shapefiles were:

- Merged and aligned with incident data.
- Converted into TopoJSON and GeoJSON formats for seamless integration with Power BI.
- Used to design static print layouts for presentation needs, complementing the interactive Power BI dashboards.

![QGIS-map](Images/QGIS%20Map-East%20Mediterranean%20Humanitarian%20Corridor.png)

*Figure 4: QGIS print layout.*

#### Challenges Overcome:
- Name Standardization: Adjusted province names (e.g., "Deir ez-Zor" → "Dayr Az Zawr").
- Projection Compatibility: Re-projected shapefiles to EPSG:4326 for consistent integration.

## 5. Assumptions & Limitations
### Assumptions
- Incident IDs are unique.
- Missing geographic values were filled using reverse geocoding and manual adjustments.
### Limitations
- Geographic completeness: Some regions rely on approximate coordinates.
- Data reliability: Incident data may be incomplete due to underreporting or discrepancies in sources, particularly in conflict zones where data collection is challenging.

## 6. Future Enhancements
### Customizable Maps
The visualizations can be tailored to specific stakeholder needs, including additional geographic regions or filtering criteria.

### Partnerships
- Collaboration with humanitarian organizations can improve the project’s accuracy and utility through data validation and additional contributions. 
- Expanding the dataset to include incidents where humanitarian aid workers were not directly affected could provide a broader context, uncovering patterns and factors contributing to overall security risks in high-risk areas. 

## 7. Conclusion
This project delivers actionable tools to enhance the safety of humanitarian aid workers in high-risk areas. The Power BI dashboard offers interactive, data-driven insights into incident types and trends, victim demographics, and geographic hotspots, while the QGIS visualizations provide detailed static maps for reporting and presentations. These tools equip security managers and humanitarian organizations to allocate resources more effectively, anticipate risks, and improve operational planning.

By integrating advanced geospatial analysis with dynamic visualization techniques, the project creates a foundation for broader applications, such as monitoring emerging threats, evaluating the effectiveness of security policies, and guiding long-term strategies. Future partnerships with humanitarian organizations and integration with broader datasets could further amplify the project's impact, enabling more comprehensive and informed decision-making across the humanitarian sector.

Explore the full **[Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiMmRkZjRkZGQtMzQ5ZS00MDI0LTljYmYtMjJiOTgwMDhmZGU0IiwidCI6IjVlNmFlYmFjLWQ1OGItNGIwYi1iMmE2LTY1YTdjYWMxMGM0NSIsImMiOjl9)** for a detailed view of the results and insights.

## 8. References
- Aid Worker Security Database. Humanitarian Outcomes. Accessed from https://aidworkersecurity.org, November 2024.
- Global Administrative Areas Database. GADM. Accessed from https://gadm.org, November 2024.
- MapShaper. Accessed from https://mapshaper.org, November 2024.
- Power BI. Microsoft Corporation. 
- Icon Map - custom visual for Microsoft Power BI. James Dales. Accessed from https://www.icon-map.com, November 2024.
- QGIS Geographic Information System. QGIS Association. Accessed from http://www.qgis.org, October 2024

## 9. Appendix
- M Code Logic: Handles missing data and name standardization.
- DAX Logic: Powers dynamic measures and visualization interactivity.
- Python Code: Used for reverse geocoding.
- Aid Worker Security Database Codebook: Published by Humanitarian Outcomes, 2021.
