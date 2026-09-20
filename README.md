# 404_not_found
Hackathon project

# GRID POINT - WAREHOUSE LOCATION OPTIMISATION

A sophisticated, full-stack spatial optimization tool for solving the Capacitated Facility Location Problem. This application dynamically clusters geographic coordinates (houses/demand points) and determines the optimal locations for supply warehouses while strictly adhering to geographic, capacity, and density constraints.

The system is split into a robust **Python Flask Backend** that handles the complex algorithmic calculations and a **Brutalist HTML/JS Frontend** that visualizes the results on an interactive True-Color OpenStreetMap.

---

## 🌟 Key Features

* **Auto-Density Discovery (Algorithm 1):** Automatically discovers the optimal number of warehouses required based on geographic spread and density requirements.
* **K-Medians Override (Algorithm 2):** Allows users to specify an exact number of target warehouses ($K$), triggering a K-Means++ initialization loop followed by Lloyd's algorithm to force an exact number of facilities.
* **Global Greedy Reallocation:** Prevents overlapping service lines. Every single point is strictly routed to its absolute closest valid facility across the entire map.
* **Real-time Map Visualization:** Renders color-coded networks, distinct warehouse markers, and failed "noise" nodes instantly using Leaflet.js.
* **In-Browser CSV Parsing:** Upload large coordinate datasets effortlessly.

---

## ⚙️ The Constraint Variables

You can adjust these parameters directly in the UI before clicking "Optimize":

1. **Max Radius (m):** The absolute maximum distance a warehouse is allowed to service. Points beyond this range become noise.
2. **Max Capacity:** The maximum number of points (houses) a single warehouse can support.
3. **Min Points:** The minimum number of nearby points required to justify building a warehouse. Areas with lower density are rejected as noise.
4. **DBSCAN Eps (m):** The internal search radius used to determine initial localized density clusters.
5. **Target Warehouses (K):** Leave blank to let the math decide, or enter a number to force the system to build exactly $K$ warehouses.

---

## Algorithm used in the backend 

First applying clustering algorithm the database is split into a set of clusters, where in each cluster has the datapoints that are located feasibly nearby.
Then inside each cluster, vectors are taken from the assumed initial warehouse position to each datapoint,
now an Error function is formulated:
**E = 1/2 ∑|Vi|^2
**where Vi represents induvial vecots
**then x,y of warehouse is updated based on
**x = x - a * dE/dx
**y = y - a * dE/dy
**till convergence 
**this leaving us with the optimal x,y for the warehouse in the given cluster


---

## 🛠️ Installation & Setup

Because this is a full-stack application, you must run the Python backend server for the frontend to work.

### 1. Prerequisites
Ensure you have Python installed on your machine. You will also need `pip` to install the backend requirements.

### 2. Install Backend Dependencies
Open your terminal or command prompt and install Flask and CORS:
```bash
pip install flask flask-cors
