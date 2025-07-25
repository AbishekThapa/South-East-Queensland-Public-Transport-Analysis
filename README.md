# South East Queensland Public Transport Analysis Pipeline

This repository contains the code for a full data pipeline and analysis of the South East Queensland (Translink) public transport network. The project demonstrates skills in ETL, database management (PostgreSQL), data cleaning, advanced SQL querying, and data visualization.

The primary script (`notebooks/main.ipynb`) automates the ingestion and cleaning of raw GTFS data, making it ready for the analysis performed in the accompanying Jupyter Notebook (`scripts_for_data_cleaning.ipynb`).


---

## Key Features

*   **Automated ETL Pipeline**: A Python script handles the extraction, transformation, and loading of raw GTFS data into a PostgreSQL database.
*   **Data Cleaning & Validation**: Implements crucial cleaning steps like handling nulls, correcting data types, removing duplicates, and standardizing text.
*   **Advanced SQL Analysis**: Uses complex SQL queries with CTEs, joins, and aggregations to uncover insights directly from the database.
*   **Comprehensive Visualization**: Leverages Matplotlib, Seaborn, and Folium to create a range of visualizations, from bar charts to interactive geospatial maps and heatmaps.
*   **Modular and Configurable**: Separates database credentials and file paths into a `config.py` file for security and ease of use.

## Technology Stack

*   **Language**: Python 3
*   **Databases**: PostgreSQL
*   **Core Libraries**:
    *   Pandas
    *   SQLAlchemy
    *   Psycopg2-binary
    *   Matplotlib
    *   Seaborn
    *   Folium
*   **Environment**: Jupyter Notebook, Git

## Project Structure

```
.
├── seq-translink-etl/data          # Directory for raw GTFS .txt files
├── images/                         # Directory for saved visualization plots
├── logs/                           # Directory for ETL log files
├── .gitignore
├── config.py                       # (Not committed) Stores DB credentials & paths
├── config.py.example               # Example configuration file
├── scripts_for_data_cleaning.ipynb # Jupyter Notebook with all queries and visualizations
├── requirements.txt                #required Dependencies lists
└── README.md
```

## Setup and Usage

Follow these steps to replicate the project environment.

### Step 1: Clone the Repository
```bash
git clone https://github.com/AbishekThapa/South-East-Queensland-Public-Transport-Analysis.git
cd South-East-Queensland-Public-Transport-Analysis
```

### Step 2: Set up Environment and Dependencies
It is highly recommended to use a virtual environment.
```bash
# Create and activate a virtual environment
python -m venv venv
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt

```

### Step 3: Set up PostgreSQL
Ensure you have a PostgreSQL server running. Create a database for this project (e.g., `translink_db`).

### Step 4: Configure the Application
1.  Rename `config.py.example` to `config.py`.
2.  Edit `config.py` with your PostgreSQL credentials and the path to your data directory.

### Step 5: Download Data
1.  Download the GTFS data from the [Queensland Government Open Data portal](https://www.data.qld.gov.au/dataset/general-transit-feed-specification-gtfs-translink).
2.  Unzip and place all `.txt` files into the `data/` directory.

### Step 6: Run the Pipeline
1.  **Execute the ETL script** to populate and clean the database:
    ```bash
    Open `main.ipynb` and run the cells to generate the analyses and visualizations.
    ```
2.  **Launch Jupyter Notebook** to run the analysis:
    ```bash
    jupyter notebook
    ```

# South East Queensland Public Transport - Interactive Dashboard

This repository showcases an end-to-end data analytics project, culminating in an interactive Power BI dashboard that analyzes the South East Queensland (Translink) public transport network. The project begins with a Python-based ETL pipeline to process raw GTFS data and concludes with a dynamic, user-friendly business intelligence tool.

**[➡️ Download the Live Interactive Dashboard Here](PoweBi_Dashboard\seq_dashboard.pbix)**

![Dashboard Screenshot](PoweBi_Dashboard\Screenshots\Dashboard.png)
---

## Dashboard Features

*   **Key Performance Indicators (KPIs):** At-a-glance cards display the total number of routes, stops, and scheduled trips across the network.
*   **Interactive Slicing & Filtering:** Users can dynamically filter the entire report by Mode of Transport ([Bus](PoweBi_Dashboard\Screenshots\bus.png), [Train](PoweBi_Dashboard\Screenshots\train.png), [Ferry](PoweBi_Dashboard\Screenshots\ferry.png), [Tram](PoweBi_Dashboard\Screenshots\ferry.png)) and by Day of the Week.
*   **Geospatial Analysis:** An interactive map plots all stop locations, providing a clear view of network coverage and density.
*   **Performance Analysis:** A series of visuals break down performance by:
    *   Top 10 most frequent routes.
    *   Busiest individual stops.
    *   Hourly trip activity, revealing daily peak and off-peak patterns.
    *   Service levels by mode and day type (weekday vs. weekend).
