Of course. Here is a comprehensive README.md file for a GitHub repository focused on the MCDA and Suitability Analysis project.

---

# Flood Risk Modelling & Suitability Analysis for Greater Accra Region using GIS-MCDA

## 📖 Project Overview

This project utilizes **Geographic Information Systems (GIS)** and **Multi-Criteria Decision Analysis (MCDA)**, specifically the **Analytic Hierarchy Process (AHP)** and **Weighted Sum** methods, to model flood risk and identify suitable areas for sustainable development in the Greater Accra Region of Ghana. The study integrates ten environmental and infrastructural variables to create comprehensive flood risk and land suitability maps. These outputs are designed to inform urban planning, disaster preparedness, and climate-resilient development strategies in line with the UN Sustainable Development Goals (SDGs).

## 🗺️ Study Area

The study focuses on the **Greater Accra Region**, Ghana's smallest but most densely populated region, which includes the national capital, Accra. Its low-lying coastal plains, rapid urbanization, and inadequate drainage infrastructure make it highly vulnerable to frequent and severe flooding.

*   **Location:** 5°30'N - 6°30'N, 0°10'W - 0°30'E
*   **Total Area:** 3,245 km² (1.4% of Ghana's land area)

## 📊 Data Sources and Processing

All spatial data were projected in the **WGS1984** coordinate system and processed in **ArcGIS Pro**. The following datasets were collected:

| Variable Category | Data Description | Source |
| :--- | :--- | :--- |
| **Response Variable** | Historical Flood Areas (Polygons, 2011-2020) | [UNU-INWEH World Flood Mapping Tool](https://floodmapping.inweh.unu.edu/) |
| **Topographic** | Digital Elevation Model (DEM) | USGS Landsat 8 Imagery |
| | Slope & Elevation | Derived from DEM in ArcGIS Pro |
| **Hydrological** | Drainage Density | Derived from DEM using Hydrology Tool |
| | Rainfall (2011-2020) | Climatic Research Unit (CRU) |
| **Land Cover** | Land Use/Land Cover (LULC) | Classified from Landsat imagery (5 classes: Water, Vegetation, Shrubland, Settlement, Bare Land) |
| **Proximity** | Distance to Rivers, Lakes, Drains, Roads | BBBike Extract Service |
| | | Euclidean Distance calculated in ArcGIS Pro |

## ⚙️ Methodology

### 1. Multi-Criteria Decision Analysis (MCDA) - AHP & Weighted Sum
The core of the flood risk modelling involved assigning weights to each factor based on its relative importance to flooding.

**A. Analytic Hierarchy Process (AHP):**
*   **Goal:** Develop an effective flood risk model.
*   **Criteria & Sub-Criteria:** Ten variables were organized into a hierarchical structure (e.g., Meteorological, Terrain, Hydrological).
*   **Pairwise Comparisons:** Experts assigned values on a scale of 1-9 to compare the importance of each variable against every other variable.
*   **Consistency Check:** The judgments were checked for consistency. The model achieved a **Consistency Ratio (CR) of 3.8%**, which is well within the acceptable limit of ≤10%.
*   **Weight Assignment:** The final weights for the flood risk model were derived from the AHP.

**Final Variable Weights for Flood Risk Model:**
| Variable | Weight |
| :--- | :--- |
| Historical Flood Data | 21.57% |
| Rainfall | 20.80% |
| Elevation | 9.90% |
| Drainage Density | 9.90% |
| Slope | 8.50% |
| Distance to Rivers | 8.97% |
| Distance to Drains | 5.99% |
| Land Use/Land Cover | 7.30% |
| Distance to Roads | 3.61% |
| Distance to Lakes | 3.46% |

**B. Weighted Sum Model:**
*   Each variable raster was **reclassified** on a scale of 1 (Very Low Risk) to 5 (Very High Risk) based on literature and domain knowledge.
*   The reclassified rasters were combined using the **Weighted Sum** tool in ArcGIS Pro, using the weights from the AHP.
*   The output is a composite flood risk map classified into five zones.

### 2. Suitability Analysis for Development
The same variables were used to identify areas suitable for future development, with flood risk acting as a constraint.

*   **Data Transformation:** Continuous variables (e.g., Rainfall, Slope, Distance to Rivers) were transformed to a common 1-5 suitability scale using various **Rescale Functions** (Logarithmic, Gaussian, Exponential, Linear, Logistic) in ArcGIS Pro to reflect their non-linear relationship with suitability.
*   **Categorical Reclassification:** The LULC layer was reclassified based on development suitability (e.g., Settlement=5 [Most Suitable], Water=1 [Least Suitable]).
*   **AHP for Suitability:** A new AHP was conducted to weight the variables for the suitability goal, resulting in a CR of 8.0%.
*   **ModelBuilder:** An ArcGIS Pro ModelBuilder workflow was created to integrate the transformed and weighted layers into a final suitability map.
*   **Site Selection:** The **Locate Regions** tool was used to identify the top 10 most suitable zones for development.

## 📈 Results and Outputs

### 1. Flood Risk Map (MCDA)
The final flood risk map delineates the Greater Accra Region into five risk categories:
1.  **Very Low Risk**
2.  **Low Risk**
3.  **Moderate Risk**
4.  **High Risk**
5.  **Very High Risk**

The map shows a strong correspondence with historical flood events, particularly in central and coastal areas, though it over-predicts risk in some western regions.
![MCDA Flood Risk Map] <div>
  <img src="https://raw.githubusercontent.com/frankraDIUM/GIS-Cartography-RS/refs/heads/main/Flood%20Risk%20Map%20with%20AHP%20and%20Weighted%20Sum.jpg"/>
</div>

### 2. Suitability Map for Development
The suitability analysis output identifies areas with the lowest flood risk and best conditions for sustainable settlement. The most suitable areas (colored green) are primarily located in parts of central, western, and southeastern Greater Accra.
![Suitability Map]<div>
  <img src="https://raw.githubusercontent.com/frankraDIUM/GIS-Cartography-RS/refs/heads/main/Suitability%20Map.jpg"/>
</div>

### 3. Comparative Analysis
The project compared the MCDA results with a separate Logistic Regression model. The analysis showed that while both models agreed on the location of the highest-risk zones (Very High risk ~1% of area), the MCDA model predicted a larger proportion of the region to be in Low to Moderate risk categories, providing a valuable complementary perspective.



## 🛠️ Usage

### Prerequisites
- **GIS Software:** ArcGIS Pro (with Spatial Analyst license)
- **AHP Tool:** Microsoft Excel (for viewing/editing AHP calculations)

### Steps to Reproduce:
1.  **Open the ArcGIS Pro Project** (`GIS/ArcGIS_Pro_Project.aprx`).
2.  **Review AHP Weights:** Examine the `AHP_Calculations.xlsx` file to understand the weighting process.
3.  **Run Weighted Sum Tool:** Use the derived weights and the reclassified rasters as inputs into the Weighted Sum tool to generate the flood risk map.
4.  **Run Suitability Model:** Open and run the Suitability ModelBuilder workflow (`GIS/ModelBuilder/`) to generate the development suitability map.

## 🎯 Conclusions and Impact

This study demonstrates the effective application of GIS-MCDA for environmental modelling and spatial planning.

*   **Informed Decision-Making:** The flood risk and suitability maps provide actionable intelligence for urban planners, disaster management agencies (e.g., NADMO), and policymakers in Ghana.
*   **Sustainable Development:** The project directly supports the achievement of **SDG 11 (Sustainable Cities and Communities)** and **SDG 13 (Climate Action)** by promoting risk-informed land use planning and climate resilience.
*   **Methodological Transparency:** The use of AHP provides a structured, defensible, and transparent framework for integrating expert knowledge into spatial decision-making.

## 🔮 Future Work

- **Incorporate Machine Learning:** Compare and integrate MCDA results with machine learning models (e.g., Random Forest) for enhanced predictive accuracy.
- **Dynamic Modelling:** Integrate climate change projections and urban growth scenarios to model future flood risk and suitability.
- **Community Engagement:** Develop a participatory GIS (PGIS) platform to incorporate local knowledge and perceptions into the model.
- **High-Resolution Data:** Utilize LiDAR data for more accurate topographic and hydrological modelling.


## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- United Nations University Institute for Water, Environment and Health (UNU-INWEH)
- US Geological Survey (USGS)
- Klaus D. Goepel for the AHP Excel Template
- Ghana Meteorological Agency (GMET) and National Disaster Management Organisation (NADMO)

---
