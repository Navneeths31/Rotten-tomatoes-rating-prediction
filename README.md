# Rotten-tomatoes-rating-prediction

In this task, we are tasked with predicting audience_rating based on the rotten tomatoes model. We have around 16638 rows and around 15 columns. 

The column 'critics_consensus' contains more than 50% missing data, so we can drop it. For the columns which have int or float types and contain missing data, we can replace the missing values by the mean of those columns. In order to do that, we create a separate function called null_check which handles the null_values. Along with that, it will also drop the column critics_consensus (and any other column whihc consists of 50% missing data which we missed).

The columns 'genre', 'directors' and 'writers' consist of common elements (i.e different movies can belong to the same genre and may have same directors or writers). In this case, we take the elements of one of those columns, for eg. genre, and we convert the objects into integers or floats.
1) We first take all the genres present in the dataset and put them into a list, called 'genre_values'
2) Then we assign a score to each movie based on it's genre - the score is the index of the genre in the list. If a movie consists of multiple genres, we take the average of the indexes of all the genres and assign it to a list called 'new_genre'
3) We convert new_genre to a dataframe

For the column 'cast' also, we can use a similar process as we did for genre, directors and writers, however, there are 2,04,103 unique cast members in total, so finding the average and creating a different dataframe with the averages is going to be time-consuming, therefore it may be better to drop that column. Similarly, the column 'studio_name' also consists of 2887 unique names, therefore it may be better to drop it.
The column 'movie_title' consists of 16106 unique titles out of a total of 16638, so almost 500 are repeated ones, we do not know any way by which we can handle these, so we drop that too.
Apart from this column, the columns movie_title, movie_info, in_theatres_date and on_streaming_date does not give us any important information as to predict audience_rating, so we drop those as well.
Along with these, we can drop the columns genre, directors and writers since we already have worked on those and just need to add the new dataframes to the dataset.

Now we need to work on the columns rating and tomatometer_status. We can see that these are categorical values, so we use OneHotEncoder to convert these to numerical data.

I used linear regression, ridge regression, decision trees and random forests on this data and used accuracy, mean absolute error, root mean square error and R2 score as parameters.

We can see that none of the models produce excellent results. None of them have even provided 50% accuracy. This is clearly stated in Decision trees when we have training accuracy of 100% and test accuracy as -0.05%, indicating a clear case of overfitting. However, there is a chance of even less scores if we drop more columns, so this is the best shot we have.
(Note: Trying Standard Scaling and using PCA resulted in even less accuracy, so I have decided not to use that.)
