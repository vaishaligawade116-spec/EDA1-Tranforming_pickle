# Titanic Data Preprocessing and Pickle Demo

This repository demonstrates how to prepare Titanic data for machine
learning using **Pandas** and **Scikit-learn**, create a reusable
preprocessing pipeline with `ColumnTransformer`, and save Python objects
as pickle files.

## Project files

  -----------------------------------------------------------------------
  File                                Description
  ----------------------------------- -----------------------------------
  `Transformer_pickle_demo.ipynb`     Jupyter Notebook containing data
                                      inspection, missing-value handling,
                                      transformer creation, and
                                      pickle-saving examples.

  `custom_function.py`                Reusable custom preprocessing
                                      functions and transformer
                                      definitions.

  `train.xls`                         Titanic training dataset supplied
                                      with this project.

  `Titanic.pkl`                       Pickled `ColumnTransformer`
                                      preprocessing configuration.

  `processed_data.pkl`                Pickled Pandas DataFrame containing
                                      the data after the notebook's
                                      missing-value handling steps.
  -----------------------------------------------------------------------

## What this project covers

1.  **Data loading and exploration** -- reads the dataset and uses
    methods such as `head()`, `tail()`, `info()`, `describe()`, and
    `isnull().sum()`.
2.  **Missing-value handling** -- fills missing values in `Embarked`
    with `"2"` and missing values in `Age` with the column mean.
3.  **Custom label encoding** -- defines `ModifiedLabelEncoder`, which
    reshapes the encoded output into a two-dimensional column.
4.  **Function transformation** -- uses `FunctionTransformer` to divide
    `Age` values by 100.
5.  **ColumnTransformer** -- applies different transformations to
    selected columns:
    -   `Sex`: One-Hot Encoding
    -   `Fare`: Standard Scaling
    -   `Embarked`: Modified Label Encoding
    -   `Age`: Custom divide-by-100 transformation
    -   `Pclass`, `SibSp`, `Parch`, `Survived`: Passed through unchanged
6.  **Pickle serialization** -- saves the preprocessing object and
    processed DataFrame to `.pkl` files.

## Requirements

Install the required packages:

``` bash
pip install pandas numpy seaborn scikit-learn matplotlib jupyter xlrd
```

`xlrd` may be needed by Pandas to read an older `.xls` Excel file.

## How to run

1.  Clone or download this repository.

2.  Keep the notebook, Python file, dataset, and pickle files in the
    project folder.

3.  Install the requirements listed above.

4.  Open Jupyter Notebook:

    ``` bash
    jupyter notebook
    ```

5.  Open `Transformer_pickle_demo.ipynb` and run the cells in order.

### Dataset filename note

The notebook currently contains:

``` python
data = pd.read_csv("train.csv")
```

The dataset included here is named `train.xls`. Either convert the Excel
file to CSV and save it as `train.csv`, or change the notebook's loading
code to:

``` python
data = pd.read_excel("train.xls")
```

## Using the custom functions

`custom_function.py` contains the custom label encoder class, the
`divide_by_100` function, and the `FunctionTransformer` objects. Keep
this file available when using pickle objects that depend on definitions
from it.

## Important implementation note

The notebook creates and saves the `ColumnTransformer` as `Titanic.pkl`.
In the notebook cells shown, the transformer is configured but is not
fitted with `fit()` or `fit_transform()` before it is saved. To save a
fitted transformer, fit it on the intended training data first, for
example:

``` python
preprocessor.fit(data)
```

Use the same preprocessing definitions and compatible package versions
when loading and using the saved object.

## Loading a pickle file

``` python
import pickle

with open("Titanic.pkl", "rb") as file:
    preprocessor = pickle.load(file)

with open("processed_data.pkl", "rb") as file:
    processed_data = pickle.load(file)
```

**Security:** Only load pickle files from sources you trust. Loading an
untrusted pickle file can execute malicious code.

## Learning outcome

After completing this project, you will understand how to inspect and
clean a dataset, apply different preprocessing techniques to selected
columns, build a reusable `ColumnTransformer`, and serialize Python
objects using pickle.
