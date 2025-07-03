# South East Queensland Public Transport Analysis Pipeline

This repository contains the code for a full data pipeline and analysis of the South East Queensland (Translink) public transport network. The project demonstrates skills in ETL, database management (PostgreSQL), data cleaning, advanced SQL querying, and data visualization.

The primary script (`main.ipynb`) automates the ingestion and cleaning of raw GTFS data, making it ready for the analysis performed in the accompanying Jupyter Notebook (`scripts_for_data_cleaning.ipynb`).


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
git clone <https://github.com/AbishekThapa/South-East-Queensland-Public-Transport-Analysis.git>
cd <South-East-Queensland-Public-Transport-Analysis>
```

### Step 2: Set up Environment and Dependencies
It is highly recommended to use a virtual environment.
```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  

# Install required packages
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
    main.ipynb
    ```
2.  **Launch Jupyter Notebook** to run the analysis:
    ```bash
    jupyter notebook
    ```
    Open `main.ipynb` and run the cells to generate the analyses and visualizations.
