# Bike Sharing Demand Regression

Predict how many bikes get rented in an hour, from weather and calendar data.

This is coursework, not research. It is Practical Work 3 from my Artificial Intelligence course at SUPMTI Rabat, taught by Pr. Soufiane Hamida. I am publishing it here as a clean, runnable record of the work.

## Data

Bike Sharing Demand, Capital Bikeshare, Washington DC, 2011 to 2012, from the UCI Machine Learning Repository. Hourly rental counts with weather and seasonal information. The notebook downloads it from UCI itself, so there is no data file to fetch by hand.

17,379 hourly records. Target is `cnt`, the number of bikes rented in that hour.

## What the notebook does

1. Loads the data and checks for missing values. There are none.
2. Removes outliers: any hour where the rental count sits more than 3 standard deviations from the mean. That drops 244 rows, leaving 17,135.
3. Maps the coded categories to labels, exactly as the practical states: season to spring, summer, fall, winter; weather to clear, misty, light rain/snow, heavy rain/snow; holiday to working day or holiday. One note: the CSV column is called `weathersit`, not `weather`. The notebook maps `weathersit`.
4. One-hot encodes the labelled categories. The practical maps them to labels but does not say how to feed them to a linear model, so this step is mine, and the notebook says so.
5. Splits 80/20 into train and test, `random_state=0`.
6. Trains three models and compares them on mean squared error and R-squared: linear regression, decision tree, random forest.

## Results

Run on the full hourly data, test set of 3,427 hours:

| Model | MSE | R-squared |
| --- | --- | --- |
| Linear regression | 16,883.84 | 0.4033 |
| Decision tree | 2,970.11 | 0.8950 |
| Random forest | 1,722.51 | 0.9391 |

The honest read: linear regression underfits here. It explains about 40 percent of the variance. The tree models do far better, and the random forest is the best of the three. In the linear model, temperature pushes rentals up and humidity pushes them down, which matches what you would expect.

## How to run

```bash
pip install pandas numpy scikit-learn matplotlib
```

Then open `bike-sharing-regression.ipynb` in Jupyter or VS Code and run it top to bottom. The notebook downloads the data itself.

## Stack

Python, pandas, NumPy, scikit-learn, Matplotlib.

## Status

Coursework practical, complete. It is a baseline, not a finished product. It treats each hour as independent and ignores time order, which is a real limit if this ever becomes more than a practical.
