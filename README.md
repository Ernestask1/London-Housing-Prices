# London Housing Prices

For this project, London house pricing data was taken and analysed. Using 'Pandas' library we can merge the London Boroughs .geojson file that contains the geographic locations of each borough to their respective names in the London Profiles dataset. This dataset contains a lot of information of each borough such as 'CrimeRate', 'BornAbroad', 'AveAge' etc..

For our analysis we will make use of the 'HousePrice' column to perform data analysis. Making use of some coding techniques, we can create a table that contains information related to housing price for each borough. _(Here a glimpse of what table structure looks like)_

![some info](https://user-images.githubusercontent.com/99913034/220478998-ce5c264b-4e36-4b91-9ffb-bbd2e663fa26.PNG)

By taking the house point density for each borough, we can create a plot to show the concentration of houses within each borough. Increasing concentration is shown for darker shades of blue.

![Boroughs](https://user-images.githubusercontent.com/99913034/220480245-42a320f7-f7c7-49d3-8ae4-ee6e8f192373.png)


The Knearest neighbours algorithm was used from the package `sklearn` in python as a machine learning tool. The first step is to scale the data so that it can be optimal for use within the algorithm. The predictor variables `east``north` and `fl_area` go through a calibrated scaler to transform them to z-scores. The tuning parameters of nearest neighbours=6, weights='uniform' and Euclidean distance metric p=2 were chosen. 
Then we initiate the response variable to be `price` and fit the regression of our 3 predictors to the scaled response variables. To optimise the turing parameters a scoring method is imported.

A grid search model is imported and we initiate the `estimator` to the nearest neighbour algorithm, scoring system is `mae` and the `param_grid` is a dictionary with keys corresponding to parameters. 

Each combination of items in the dictionary will be tested, and combination with the best `mae` will be selected. The selected values will be saved on the `opt_nn` which can be though of as a regression object that has fit and predict methods.

A pipeline algorithm is then implemented because of its convenience to calibrating models and making predictions using the original data, rather than manually re-scaling the data set every time. A grid search algorithm is then implemented in a similar way to the `opt_nn` which also fits our predictors and the response variable. 

### 3D graph for average floor size

To now visualise the outcome, a grid is created. This grid is bounded in a space defined by the spatial range of values of `èast` and `north`. This grid array is assigned the value of average floor size of 92.88 sq meters. The grid can now be used for predict method and the response variable `price` is also made into a grid to be used in the method. The `hp_pred` dataset is now re-shaped to have the same dimensions and is ready for graphing.


![House price per mean floor area](https://user-images.githubusercontent.com/99913034/220473244-ca866ad2-4c5d-43b1-b60c-7035c149581d.png)

Here we can see a big variation in house price for average floor area. This tells us that the spatial component in this dataset is a major predictor for house prices. If it were not to be the case, we would see uniform distribution throughout. An interesting thing to note is that the price does not increase gradually based on spatial coordinates, but rather spikes up near the centre indicated by the redness part of the graph. This is a clear indicator that house prices are not based upon the floor area and change heavily based on their geohraphical location.

We can also notice some edge effects present in this graph. These are located at the edges of the points because the Knearest neighbour algorithm takes the nearest neighbours located inwards. Most of these locations on the edges have neighbours outside of the spatial bounds which is why we see "edges" that look flat. The neighbours outside of the bounds are not taken into the algorithm and so this is the effect that we see. This means that the predicted price of houses located on the edges are less accurately represented than the majority of points near the middle of the graph.

### Floor area of 75 sq metres

![75](https://user-images.githubusercontent.com/99913034/220475851-6e0ac55c-3f66-4998-98c3-8bbfb004db71.png)

For houses of floor area of 75 sq meters, we see a similar graph to the average floor size. The steep slopes are visible in a similar way to the graph above. We see that below average sized living spaces have their prices varied signficantly by location. Edge effects are visually present in a similar way to the graph above.

### Floor area of 125 sq metres

![125](https://user-images.githubusercontent.com/99913034/220475974-5f42901b-22dd-45f7-90a6-3ee3b11e0581.png)

For living spaces of 125 sq metres (slightly above average) we again see similar spatial patterns in house price. House price remains heavily space dependent but we also notice the slopes decreasing slightly when compared to the steepness of average floor size. Edge effects are present.

### Floor area of 250 sq metres

![250](https://user-images.githubusercontent.com/99913034/220476078-9c3e64ed-34d3-400c-826c-a4a80724e40b.png)

For our final choice of floor area = 250 sq metres we can see the spatial variation of house price looks very different to the previous three plots. The changes in house price between locations increase/decrease more gradually rather than sharply as seen before. This tells us that the bigger living spaces in London are not as affected spatially compared with the average sized living locations. Although we still see some spikes in this graph, the degree to which prices vary by location is a lot less than previously seen.

Edge effects in this graph are much more prominent than what we saw previously. We can see the flat jagged edges continue on much further into the graph. This is because there are a lot less living spaces at 250 sq metres than previous plots. Thus the nearest neighbours are much more spread out with longer distances causing the edge effects to drag out much further into the graph.

# Conclusion

House prices in London vary by location. In particular the average sized living spaces see big variations in price whereas the degree to which the bigger houses/apartments are affected is a lot less. This is seen visually in our graphs and the slopes that indicate price variation reflect this conclusion. The Knearest neighbour machine learning algorithm is an ideal tool to perform this analysis.
