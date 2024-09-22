# GBIF Metadata Analysis and Visualization

## Overview

This script performs an analysis of metadata from the Global Biodiversity Information Facility API, visualizes the data, and generates useful outputs such as networks, choropleth maps, word clouds, and markdown summaries.

### Features

- **Fetch Metadata from GBIF API**: Retrieves metadata for a list of DOIs from the GBIF API.
- **Data Processing**: Cleans and organizes data from CSV files, calculates statistics, and enriches metadata with additional information such as taxon names and country names.
- **Network Creation and Visualization**: Builds networks of keywords and topics and visualizes them using NetworkX and Matplotlib.
- **Markdown and PDF Generation**: Creates detailed Markdown summaries for each publication and converts them into PDF format.
- **Geospatial Visualization**: Generates a global choropleth map highlighting the number of publications by researchers' countries.
- **Word Cloud Generation**: Creates word clouds based on publication abstracts and keywords.

## Requirements

The script requires the following Python packages:

- `pandas`
- `requests`
- `networkx`
- `matplotlib`
- `tqdm`
- `pypandoc`
- `pycountry`
- `re`
- `basemap`
- `wordcloud`


## Setup

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Ensure that you have the required CSV files:
   - `KYMS.csv`: Contains the GBIF data with DOIs from scientific literature and associated GBIF IDs of cited specimens creates from the script linkLitToGbifId.
   - `download_summary.csv`: Contains download keys and total records.

3. Create a directory named `publication_markdowns` to store the Markdown and PDF files.

4. Update the paths in the script as needed:
   - `file_path` for the main data CSV file.
   - `download_summary_path` for the download summary CSV file.
   - `output_excel_path` for saving the processed data.
   - `output_dir` for storing Markdown and PDF files.

## Usage

### 1. Data Preprocessing and Metadata Fetching
The script reads the CSV files, calculates the number of GBIF IDs associated with each DOI, and fetches metadata from the GBIF API. The relevant data is stored in a DataFrame and saved to an Excel file.

### 2. Network Creation
The script creates networks based on keywords and topics extracted from the metadata. These networks are saved as GraphML files for further analysis.

### 3. Visualization
- **Keyword Network and Topic Network**: Visualizes the relationships between keywords and topics using NetworkX.
- **Choropleth Map**: Generates a map showing the distribution of publications by researchers' countries.
- **Word Clouds**: Creates word clouds from publication abstracts and keywords.

### 4. Markdown and PDF Generation
Creates a detailed Markdown file for each publication with all relevant metadata, and converts it to a PDF file using a LaTeX template.

### 5. Running the Script
Run the script in a Python environment with all dependencies installed. For large datasets, make sure to handle API rate limits and possible errors appropriately.

```bash
python gbif_metadata_analysis.py
```

## Outputs

- **Excel File**: `gbif_literature_data.xlsx` containing processed metadata.
- **GraphML Files**: `keyword_network.graphml` and `topic_network.graphml`.
- **Markdown Files**: Individual Markdown files for each publication stored in the `publication_markdowns` directory.
- **PDF Files**: Converted PDF files for each publication in the `publication_markdowns` directory.
- **Images**:
  - `publications_by_country.png`: Choropleth map of publications by country.
  - `wordcloud_abstracts.png`: Word cloud based on publication abstracts.
  - `wordcloud_keywords.png`: Word cloud based on keywords.

## Troubleshooting

- **Font Issues**: If you encounter warnings about missing glyphs, ensure that you have a font installed that supports the characters being used. You can modify the font settings in the script. Having said that, there is not much to be gained from fixing all of these warnings.
- **API Rate Limits**: If the GBIF API rate limits your requests, you may need to increase the delay between requests or handle the `429` status code more robustly.