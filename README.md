## Surrogate Modelling of Benzene-Toluene Distillation using Peng Robinson method in DWSIM and Machine Learning Models.

# Project Overview
This project uses the method of surrogate modelling to generate a dataset worth 5000 points, taking control of DWSIM file with a flowsheet of a distillation column separating a Benzene-Toluene mixture using Peng Robinson EOS. By using DWSIM COM bridge, the 7 input parameters (Feed temperature, Feed pressure, Liquid feed composition (Benzene), No. of trays, Feed input tray, Reflux ratio and Bottoms withdrawal rate(W)) were used to calculate the 4 output parameters (Condenser Duty, Reboiler Duty, Distillate composition (Benzene) and Bottom composition (Toluene).) This data is used to model 3 ML models: Artificial Neural Network (ANN), Support Vector Regressor (SVR) and Random Forest (RF).

# Repository Structure
* **`data/`**
  * `DWSIM_ML_Dataset.csv` : 5000-row dataset generated via COM bridge.
* **`docs/`**
  * `Report.pdf` : Full technical documentation and methodology.
* **`models/`**
  * `Distillation_MLP.pkl` : Saved neural network model.
  * `Distillation_SVR.pkl` : Saved Support Vector Regressor model.
  * `Scaler_X.pkl` / `Scaler_Y.pkl` : Input/output scalers for the ANN.
* **`notebooks/`**
  * `Dataset_Generation.ipynb` : Script automating DWSIM data generation.
  * `Model_Training.ipynb` : Script to train the ANN, SVR, and RF models.
* **`simulation/`**
  * `Benzene_Toluene_Column.dwxmz` : DWSIM flowsheet utilizing Peng-Robinson EOS.
* `README.md`

# Prerequisites and Dependencies
Python 3.13
DWSIM v9.0.5
`pythonnet`, `scikit-learn`, `pandas`, `numpy`, `matplotlib`, `joblib`.

# Installation and Setup
1. Download this repository to a local directory.
2. Open terminal / command prompt.
3. Install the required libraries by running: `pip install pythonnet scikit-learn numpy pandas matplotlib joblib`
4. To run this script successfully, ensure that FOSSEE.dwxmz is located in the exact directory specified in the notebook.

# Execution Instructions
1. Open DWSIM v9.0.5,  go to `File > Open`, and select `FOSSEE.dwxmz` to view the base flowsheet and thermodynamic setup.
2. To run the data generation script successfully, ensure that `FOSSEE.dwxmz` is located in the exact directory specified in `Dataset_Generation.ipynb`. Run all cells to launch the COM-bridge and generate a new CSV.
3. Open `Model_Training.ipynb` and run the cells. The script is instructed to load `DWSIM_ML_Dataset.csv` directly from the same folder to train the models and output metrics.
4. Load the `.pkl` files using `joblib`.

# Key Results
Artificial Neural Network (ANN): Best overall performer with a distillate composition (Benzene) MAE of 0.002.
Support Vector Regressor (SVR): Performance close to ANN with distillate composition (Benzene) MAE of 0.005.
Random Forest (RF): Worst performing model with a distillate composition (Benzene) MAE of 0.025.
