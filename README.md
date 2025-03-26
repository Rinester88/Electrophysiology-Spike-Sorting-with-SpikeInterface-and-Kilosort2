![CD8945E9-3732-4D4F-958A-DC3AD615E4EF](https://github.com/user-attachments/assets/6dc28888-2582-4c3e-b55a-5865d5ea3b58)
# Electrophysiology-Spike-Sorting-with-SpikeInterface-and-Kilosort2
Electrophysiology spike sorting is a critical step in analyzing neural data recorded from the brain using techniques like multi-electrode arrays (MEA)
# Project Overview

This project provides a streamlined pipeline for preprocessing electrophysiology data and performing spike sorting using the SpikeInterface library and Kilosort2 spike sorting algorithm. It includes the following steps

	1.	Motion correction and preprocessing of electrophysiology data.
	2.	Application of Kilosort2 for spike sorting neural data.
	3.	Visualization of sorted spikes.

By using SpikeInterface and Kilosort2, this project enables efficient handling of large-scale neural data and provides a flexible interface for users working with spike sorting.

⸻

Libraries and Dependencies

This project relies on the following libraries and tools:
	•	SpikeInterface: Python library for electrophysiology data handling, including tools for spike sorting and visualization.
	•	Kilosort2: Spike sorting algorithm designed for high-throughput electrophysiology data.
	•	SpikeWrap: A wrapper around SpikeInterface to simplify preprocessing, spike sorting, and data management.

Installation

 # 1.	Clone the Repository

 ```
git clone https://github.com/your-username/electrophysiology-spike-sorting.git 
     cd electrophysiology-spike-sorting
```

# 2.	Install Dependencies:
  You can install the required Python dependencies by running

```
pip install -r requirements.txt
```
# 3.	Setting Up Kilosort2 
  Clone the Kilosort2 repository

```
git clone https://github.com/MouseLand/Kilosort2

```
•	Set the KILOSORT2_PATH environment variable to point to the Kilosort2 directory

```
export KILOSORT2_PATH="/path/to/Kilosort2"
```
# 4.	Verify Installation:
 Run the sample pipeline to check if everything is set up properly

 ```
python scripts/run_sample_pipeline.py

 ```

# Pipeline Overview

This project follows a structured pipeline involving the following steps 

## 1. Data Preprocessing

The preprocessing step includes motion correction, data normalization, and filtering to clean the data and prepare it for spike sorting. The core preprocessing script is as follows:

```
# Preprocessing the data
from spikeinterface import extractors as se
from spikeinterface.preprocessing import bandpass_filter, common_reference

# Load raw data
recording = se.BinaryRecordingExtractor('path_to_your_raw_data')

# Apply bandpass filter to the data (e.g., 300-6000 Hz for spike sorting)
filtered_recording = bandpass_filter(recording, freq_min=300, freq_max=6000)

# Apply common reference subtraction to reduce noise
common_ref_recording = common_reference(filtered_recording, reference='mean')

```

## 2. Spike Sorting with Kilosort2

After preprocessing, the data is passed to Kilosort2 for spike sorting. This step is executed using SpikeInterface and requires setting up the KILOSORT2_PATH variable to point to the directory where Kilosort2 is installed.

```
from spikeinterface.sorters import run_sorter

# Define the sorter name and the preprocessed data
sorter_name = 'kilosort2'
sorting = run_sorter(sorter_name, common_ref_recording)

```

## 3. Result Visualization

After spike sorting, the sorted spikes are saved, and you can visualize them with SpikeInterface widgets. Here’s an example of how to load and visualize the sorted output:

```
from spikeinterface.widgets import SortingView

# Load the sorting result
sorting = si.load_sorting("/path/to/sorting_output")

# Visualize the sorting output
sorting_view = SortingView(sorting)
sorting_view.show()

```
# Project Structure

Here is an overview of the project directory structure

```
electrophysiology-spike-sorting/
│
├── Kilosort2/                  # Kilosort2 repository directory
├── data/                       # Folder for raw electrophysiology data
├── results/                    # Folder for sorting results
├── notebooks/                  # Jupyter notebooks for interactive analysis
├── scripts/                    # Python scripts for preprocessing, sorting, and analysis
│   ├── preprocess.py           # Data preprocessing and cleaning script
│   ├── run_sample_pipeline.py  # Example script to run the full pipeline
│
├── environment.yml             # Conda environment file
├── requirements.txt            # Python dependencies file
├── README.md                   # Project documentation

```

# Usage
## ]1.	Preprocess Data:
  You can preprocess your electrophysiology data by running the following command

```
python scripts/preprocess.py --input /path/to/raw_data --output /path/to/output_data

```
## 2.	Run Spike Sorting:
Once the data is preprocessed, run Kilosort2 for spike sorting

```
from spikeinterface.sorters import run_sorter

sorter_name = 'kilosort2'
sorting = run_sorter(sorter_name, corrected_recording)
```

## 3.	View Sorting Results:
After spike sorting is complete, you can visualize the results

```
from spikeinterface.widgets import SortingView

sorting = si.load_sorting("/path/to/results")
sorting_view = SortingView(sorting)
sorting_view.show()
```
# Troubleshooting
•	Missing Dependencies: If you see missing package errors, ensure the correct environment is activated, and all dependencies are installed. Use pip install -r requirements.txt or conda env create -f environment.yml.
•	Kilosort2 Path Issue: If you get errors stating that Kilosort2 cannot be found, verify that the KILOSORT2_PATH environment variable is correctly set
```
export KILOSORT2_PATH="/path/to/Kilosort2"

```

# Contributing

## Contributions are welcome! Here’s how you can contribute to the project:
1.	Open Issues: For bug reports or feature requests.
2.	Fork and Pull Requests: If you want to add new features or fix bugs, please fork the repository and submit a pull request.
3.	Testing: Ensure your changes are well-tested and do not break existing functionality.

# Python Environment Files
•	environment.yml: A conda environment configuration file that lists all the dependencies needed for the project. This file is used to create a specific environment with all the necessary libraries, including SpikeInterface, Kilosort2, and other dependencies.
•	requirements.txt: A pip requirements file for installing Python dependencies. This is often used for projects that don’t rely on conda or where users prefer installing libraries directly via pip.

```
name: spike_sorting_env
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.8
  - numpy
  - scipy
  - spikeinterface
  - matplotlib
  - pandas
  - scikit-learn
  - pip
  - pip:
      - kilosort2
```
# 2. Preprocessing Scripts
•	preprocess.py: A script that handles data preprocessing tasks like filtering and applying common reference subtraction. This prepares raw electrophysiology data for spike sorting.
•	run_sample_pipeline.py: A sample script to demonstrate the full pipeline, including preprocessing, spike sorting, and visualization. This file provides an example of how to run the entire workflow.

# 3. Spike Sorting Scripts
•	sorting.py: This script will handle the process of running the spike sorter (in this case, Kilosort2) on the preprocessed data. It is responsible for invoking the sorter and saving the results.
•	run_sorter.py: This is the part where the Kilosort2 algorithm is triggered using the SpikeInterface API.

# 4. Visualization Files
•	visualize.py: A script that contains code to visualize the raw data, spike trains, and sorted clusters. This script can be used to view the results of the spike sorting process.
•	widgets/: A directory containing visualization helper files (like custom views for sorting and spike waveform plots).

# 5. Data Files
•	Raw Data: Files containing electrophysiology data (e.g., .bin, .nwb, .dat, etc.). This data can be raw or preprocessed depending on the needs of the user.
•	results/: This directory contains the output from the spike sorting process, including spike train data, clustering results, and sorted spike waveforms.
•	output/: Contains temporary output or sorted results that are generated by running scripts.

# 6. Configuration Files
•	config.json: A JSON configuration file to store customizable parameters like file paths, filter settings, and spike sorting parameters.

```
{
  "raw_data_path": "/path/to/raw/data",
  "preprocessed_data_path": "/path/to/preprocessed/data",
  "kilosort2_path": "/path/to/Kilosort2",
  "sorting_params": {
    "num_channels": 128,
    "sampling_rate": 30000,
    "high_pass_filter": 300,
    "low_pass_filter": 6000
  }
}
```

# Directory Structure Overview

The structure of the repository would look like this
```
electrophysiology-spike-sorting/
│
├── Kilosort2/                   # Kilosort2 repository directory (cloned from GitHub)
├── data/                        # Folder for raw electrophysiology data
├── results/                     # Folder for sorting results
├── notebooks/                   # Jupyter notebooks for interactive analysis
├── scripts/                     # Python scripts for preprocessing, sorting, and analysis
│   ├── preprocess.py            # Data preprocessing and cleaning script
│   ├── run_sample_pipeline.py   # Example script to run the full pipeline
│   ├── sorting.py               # Spike sorting script
│   └── visualize.py             # Visualization script
│
├── widgets/                     # Visualization helper files
│   ├── RecordingView.py         # Raw data visualization
│   ├── SpikeTrainView.py        # Spike train visualization
│   └── ClusterWaveformView.py   # Cluster waveform visualization
│
├── environment.yml              # Conda environment file
├── requirements.txt             # Python dependencies file
├── config.json                  # Configuration file
├── README.md                    # Project documentation
├── LICENSE                      # License file
└── .gitignore                   # Git ignore file
```


