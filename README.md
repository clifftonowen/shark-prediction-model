# Probabilistic Shark Habitat Prediction Model

## Project Synopsis
This project implements a probabilistic model to predict the movement patterns and long-term habitats of Great White Sharks (Carcharodon carcharias) using satellite telemetry data. By leveraging a Discrete-Time Markov Chain, the model analyzes historical ARGOS satellite tracks to forecast both future locations and general high-density areas (hotspots).

The model is designed to be flexible, allowing for analysis of the entire shark population or specific demographic subgroups (e.g., adult females, juvenile males), providing a powerful tool for ecological research and conservation planning.

## Key Features
- Data Standardization: Includes a preprocessing script to clean raw, irregular satellite pings into consistent daily-averaged location data.

- Long-Term Habitat Prediction: Calculates the steady-state vector of the Markov Chain to identify and visualize the most probable long-term habitats and migratory corridors.

- Time-Specific Forecasting: Predicts the probability distribution of a shark's location after a specific number of days from a known starting point.

- Demographic Filtering: Allows for the modeling of specific subgroups by filtering the dataset based on shark sex and maturity levels.

- Dynamic Visualization: Generates clear and informative heatmaps for all predictions, with dynamically generated titles and filenames for easy comparison of different model runs.

## Methodology
The model is built on the principles of a Discrete-Time Markov Chain, where the ocean is discretized into a grid of possible locations (states).

- State Definition: The total geographical area covered by the dataset is divided into a uniform N x N grid. Each cell in this grid represents a unique state a shark can occupy.

- Transition Probability Matrix (P): By analyzing the historical daily movements from the standardized dataset, a transition matrix is constructed. The entry P_ij represents the probability of a shark moving from state i to state j in one day.

- Steady-State Prediction (π): To predict long-term habitats, the model calculates the steady-state vector, π, which is the unique probability vector that satisfies the equation πP=π. This is achieved numerically by raising the transition matrix to a large power (P^n as n→∞). The resulting vector provides the long-term probability of finding a shark in any given state.

- Time-Specific Prediction (v_t​): To forecast a location after a specific number of days, the model uses the formula v_t​ = v_0 P^t, 

Where: 
- v_0 is the initial state vector (a vector with a 1 at the starting state and 0s elsewhere).
- t is the number of days into the future.
- v_t is the resulting probability vector of the shark's location at day t.

## Project Structure

- shark_prediction_model.py # Main script to build models and generate predictions.
- standardize_data.py       # Preprocessing script to clean and standardize raw data.
- shark_data.csv            # Raw satellite telemetry data (input).
- *.png                     # Output prediction heatmaps.
- README.md                 # This file.

## Prerequisites
- Python 3.x

- Pandas

- NumPy

- Matplotlib

- Seaborn

### Install the required libraries:
pip install pandas numpy matplotlib seaborn

## Execution Steps
- Place Your Data: Ensure your raw tracking data is in a CSV file named shark_data.csv in the root directory.

- Standardize the Data: Run the preprocessing script first. This will generate the clean, daily-averaged data file needed by the main model.

python standardize_data.py

You can also modify this script to generate datasets for specific subgroups (e.g., only adult females).

- Run Predictions: Execute the main prediction model.

python shark_prediction_model.py

## Data Source
This analysis is based on the "South African White Shark ARGOS Tracks" dataset.

Citation: Kock, A., Johnson, R., O'Riain, J., & Dicken, M. (2021). South African White Shark ARGOS Tracks (1.0) [Data set]. Zenodo. https://www.google.com/search?q=https://doi.org/10.5281/zenodo.5575189

Source: https://zenodo.org/records/5575189