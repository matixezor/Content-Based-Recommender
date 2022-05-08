## Hotel Content Based Recommender
### Project description
This project tries to solve the problem of recommending the best reservation option for a specific user.    
The goal was to train a content based recommender to recommend a stay for a specific user based on various user and items(rooms) features.

User features are the average values of given buckets: `length_of_stay_bucket`, `room_segment` and `n_people_bucket`.   
They were mapped to numerical values in the following manner:
```
'n_people_bucket': ['[1-1]', '[2-2]', '[3-4]', '[5-inf]'] -> 'n_people_bucket': [1, 2, 3, 4]
```
Perhaps it would've been better to map them back to original preprocessed values, but due to the lack of time to go through the tuning process again, the idea was abandoned/postponed.  
Item features were one hot encoded with additional columns indicating if a specific item bucket is an extreme value(min or max).  

When preparing the users_df in the recommender's recommend method, users with no features have them initialized as average values.  
This way the recommender treats a new user as an average user.

Various models were trained and tuned such as:
* Linear Regression model
* Random Forest Regressor model
* Gradient Boosting Regressor model

The results are not satisfying which suggests that user features could've been prepared better(perhaps mapping buckets back to original data).   
Trained models did not outperform the amazon recommender.

The results:
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right">
      <th></th>
      <th>Recommender</th>
      <th>HR@1</th>
      <th>HR@3</th>
      <th>HR@5</th>
      <th>HR@10</th>
      <th>NDCG@1</th>
      <th>NDCG@3</th>
      <th>NDCG@5</th>
      <th>NDCG@10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>RandomForestCBUIRecommender</td>
      <td>0.006449</td>
      <td>0.014936</td>
      <td>0.020367</td>
      <td>0.030550</td>
      <td>0.006449</td>
      <td>0.011492</td>
      <td>0.013742</td>
      <td>0.017072</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XGBoostCBUIRecommender</td>
      <td>0.005092</td>
      <td>0.017651</td>
      <td>0.024100</td>
      <td>0.032587</td>
      <td>0.005092</td>
      <td>0.012705</td>
      <td>0.015334</td>
      <td>0.018104</td>
    </tr>
    <tr>
      <th>2</th>
      <td>LinearRegressionCBUIRecommender</td>
      <td>0.005431</td>
      <td>0.011881</td>
      <td>0.016972</td>
      <td>0.023082</td>
      <td>0.005431</td>
      <td>0.009100</td>
      <td>0.011219</td>
      <td>0.013250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AmazonRecommender</td>
      <td>0.044128</td>
      <td>0.118805</td>
      <td>0.160896</td>
      <td>0.221656</td>
      <td>0.044128</td>
      <td>0.086755</td>
      <td>0.104347</td>
      <td>0.123980</td>
    </tr>
  </tbody>
</table>

### Requirements 
1. (Optional) Create a new environment with Python 3.8:  
`python -m venv envName`
2. (Optional) Activate the created environment:  
`myvenv\Scripts\activate`
3. Install required libraries by running this command in project's root directory:  
`pip install -r requirements`
4. Run jupyter notebook:  
`jupyter notebook`
6. You're all set! There are two jupyter notebooks:   
* Data preparation one: `project_1_data_preparation.ipynb`
* User and item features generation. Models training and tuning. Final evaluation: `project_1_recommender_and_evaluation.ipynb`
