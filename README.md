# KAN-ANN-for-STLF

## Overview

This documentation provides details on the implementation of "A Hybrid KAN-ANN based Model for Interpretable and Enhanced Short-term Load Forecasting".
## Dataset Source

The dataset used for this implementation can be found at [https://github.com/dafrie/lstm-load-forecasting](https://github.com/dafrie/lstm-load-forecasting). This repository contains electricity load forecasting data for Switzerland, along with related weather and calendar information.

## Environment Setup

To set up the environment for running the KAN-NN-for-STLF model, follow these steps:

1. **Create a new Conda environment**:
   ```bash
   conda create -n kan python=3.9.19
   conda activate kan
   ```

2. **Install required packages**:
   ```bash
   pip install pykan==0.2.8 matplotlib==3.6.2 numpy==1.24.4 scikit_learn==1.1.3 setuptools==65.5.0 torch==2.2.2 tqdm==4.66.2 xgboost==2.1.1
   ```

   **Note**: Since the dataset and its processing code originate from the `lstm-load-forecasting` repository, you may also need to install:
   ```bash
   pip install pandas==2.2.2 beautifulsoup4==4.12.3
   ```

   **Note**: The version numbers listed are provided as an example; check for the latest stable versions or compatibility with your system.

3. Some modification for pykan 

   In the `prune_node` function in the source code, we changed `auto_save` to `False`.  
   
   In the `fit` function, we annotated the following code to avoid printing internal information:  
   
   ```python
   # if _ % log == 0:
   #     if display_metrics == None:
   #         pbar.set_description("| train_loss: %.2e | test_loss: %.2e | reg: %.2e | " % (torch.sqrt(train_loss).cpu().detach().numpy(), torch.sqrt(test_loss).cpu().detach().numpy(), reg_.cpu().detach().numpy()))
   #     else:
   #         string = ''
   #         data = ()
   #         for metric in display_metrics:
   #             string += f' {metric}: %.2e |'
   #             try:
   #                 results[metric]
   #             except:
   #                 raise Exception(f'{metric} not recognized')
   #             data += (results[metric][-1],)
   #         pbar.set_description(string % data)
   ```
   
   In the `prune_input` function, we also modified it to return `input_mask` alongside the model:  
   
   ```python
   return model2, input_mask
   ```

4. **Using Virtual Environments in Jupyter Notebook and Python**：
   Please see this website to use the "kan" vitual environment in Jupyter Notebook: https://stackoverflow.com/questions/42449814/running-jupyter-notebook-in-a-virtualenv-installed-sklearn-module-not-available

## Usage

### Running the Model

To run the model, follow these steps:

1. **Open the Jupyter Notebook**:
   Use the Jupyter Notebook to open the file `"NN+KAN-SPRING.ipynb"`.

2. **Execute the code**:
   Execute the code line by line to run the model and generate the forecast results.

### Attention

- **Reproducing Results**: If you aim to reproduce the results reported in the paper, please ensure not to change any parameters in the model configuration.
- **Exploration and Improvement**: If you wish to explore and potentially improve the model's accuracy, feel free to modify the parameters and experiment with different settings.

