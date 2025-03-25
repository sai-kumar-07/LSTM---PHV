# LSTM-PHV Project

This project implements the LSTM-PHV model for predicting human-virus protein-protein interactions.

## Project Structure
- `data/`: Contains input data files such as positive and negative interactions.
- `models/`: Stores trained models.
- `scripts/`: Contains Python scripts for data processing, training, and evaluation.
- `notebooks/`: Jupyter notebooks for exploratory data analysis.
- `results/`: Stores results such as evaluation metrics and predictions.

## Setup Instructions
1. Clone the repository.
2. Install required Python packages:
3. Place the input data files in the `data/` directory.
4. Run the scripts in the `scripts/` directory to process data, train the model, and evaluate performance.

## Usage
- Run `scripts/data_processing.py` to preprocess the data.
- Run `scripts/train_and_evaluate.py` to train and evaluate the LSTM-PHV model.

### Requirements File
- torch==2.0.1
- numpy==1.24.3
- pandas==2.0.2
- scikit-learn==1.3.0
