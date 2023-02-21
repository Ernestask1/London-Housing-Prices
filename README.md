# London Housing Prices

For this project, London house pricing data was taken and analysed. The Knearest neighbours algorithm was used from the package `sklearn` in python as a machine learning tool. The first step is to scale the data so that it can be optimal for use within the algorithm. The predictor variables `east``north` and `fl_area` go through a calibrated scaler to transform them to z-scores. The tuning parameters of nearest neighbours=6, weights='uniform' and Euclidean distance metric p=2 were chosen. 
Then we initiate the response variable to be `price` and fit the regression of our 3 predictors to the scaled response variables. To optimise the turing parameters a scoring method is imported.

A grid search model is imported and we initiate the `estimator` to the nearest neighbour algorithm, scoring system is `mae` and the `param_grid` is a dictionary with keys corresponding to parameters. 

Each combination of items in the dictionary will be tested, and combination with the best `mae` will be selected. The selected values will be saved on the `opt_nn` which can be though of as a regression object that has fit and predict methods.

A pipeline algorithm is then implemented because of its convenience to calibrating models and making predictions using the original data, rather than manually re-scaling the data set every time. A grid search algorithm is then implemented in a similar way to the `opt_nn` which also fits our predictors and the response variable. 

### 3D graph for average floor size

To now visualise the outcome, a grid is created. This grid is bounded in a space defined by the spatial range of values of `èast` and `north`. This grid array is assigned the value of average floor size of 92.88 sq meters. The grid can now be used for predict method and the response variable `price` is also made into a grid to be used in the method. The `hp_pred` dataset is now re-shaped to have the same dimensions and is ready for graphing.


![House price per mean floor area](https://user-images.githubusercontent.com/99913034/220473244-ca866ad2-4c5d-43b1-b60c-7035c149581d.png)

Here we can see a big variation in house price for average floor area. This tells us that the spatial component in this dataset is a major predictor for house prices. If it were not to be the case, we would see uniform distribution throughout. An interesting thing to note is that the price does not increase gradually based on spatial coordinates, but rather spikes up near the centre indicated by the redness part of the graph. This is a clear indicator that house prices are not based upon the floor area and change heavily based on their geohraphical location.

We can also notice some edge effects present in this graph. These are located at the edges of the points because the Knearest neighbour algorithm takes the nearest neighbours located inwards. Most of these locations on the edges have neighbours outside of the spatial bounds which is why we see "edges" that look flat. The neighbours outside of the bounds are not taken into the algorithm and so this is the effect that we see. This means that the predicted price of houses located on the edges are less accurately represented than the majority of points near the middle of the graph.
