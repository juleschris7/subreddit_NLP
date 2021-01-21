# Classification modeling of two subreddits: r/DungeonsAndDragons & r/Warhammer40k
## Problem Statement
The goal of this project is to create a model that can accurately determine which subreddit, of two, a post came form: r/DungeonsAndDragons, r/Warhammer40k.
## Data
Data was scraped from the site Reddit. Titles of posts from two subreddits, r/DungeonsAndDragons and r/Warhammer40k, will be used to train and test the data which contain text for titles and for the body of each post. Posts from two additional subreddits, r/DnD and r/40k, will also be used to assess the model. These alternative subreddits are analagous to the original ones selected in order to test the model on a larger data set. The final training data set had 1724 rows and 954 columns and the test set had 850 rows and 954 columns.

![distribution_word_count.png](https://git.generalassemb.ly/juleschris7/project_3/blob/master/images/distribution_word_count.png)

## Methodology
There were no missing values in the data set of with title. However posts with a missing value in the "body" column were converted to "999" in that column. I also created a column for title word count and body word count. The target column for each subreddit was converted to numbers: posts from r/DungeonsandDragons were converted to 0 and posts from r/Warhammer40k were converted to 1.

## Exploratory Data Analysis
    -Data cleaning
        -Used CountVectorizer to create feature and remove stop words
        -Looked at word counts of most frequently appearing words, added more words to stop words list
        -lemmatized words
        -changed token pattern to keep numbers toget
    -Data checking
        -added word pairs to the list of single words
        -excluded words used less than 3 times
    -The same process was used on the dataset from the alternative subreddit.
After using the process described above the most frequently used words across the corpus made good features for the classification models.

![word_use_per_group.png](https://git.generalassemb.ly/juleschris7/project_3/blob/master/images/word_use_per_group.png)


## Modeling
Multinomial Naïve Bayes, Random Forest, and AdaBoost models were all used to predict the subreddit for each post. Naïve Bayes resulted in the highest accuracy and therefore I used a GridSearch to try and further improve on this model and test on an unseen data set.

## Results
GridSearching over produced the best accuracy scores:
Training accuracy score: 0.93852
Testing accuracy score:  0.85882
However all models including this one were overfit, indicating high variance. This model continues to suffer from over predicting r/Warhammer40k subreddit as the other models have. Using the specificity score using r/Warhammer40k as the positive category relative to sensitivity indicates that the model is over predicting the sub reddit r/Warhammer40k and underpredicts r/DungeonsAndDragons:

Specificity: 0.8137
Sensitivity: 0.9038
Precision:   0.8297

When testing this model on the alternative data set had a similar accuracy score to the testing accuracy: 0.8589

![gs_con_mat.png](https://git.generalassemb.ly/juleschris7/project_3/blob/master/images/gs_con_mat.png)

The confusion matrix above shows that even on the data from the alternative subreddits this model continues to over predict r/40k

## Conclusions & Next Steps
This final model makes has a good initial accuracy at guessing which subreddit a post is likely to be related to. This reddit does well given limited text. Investigating the posts that were misclassifid to see if a human would have an easier time classifying them would be a good step to indicate features that the model is not picking up on. To improve this score in the future the next step would be an analysis of the body rather than just title. Since much of the content posted on these pages is art it would be worth analysing the images as well to get the best accuracy.

## References

https://lifehacker.com/a-beginners-guide-to-reddit-1798643829

https://www.reddit.com/

https://www.reddit.com/r/Warhammer40k/

https://www.reddit.com/r/DungeonsAndDragons/

https://www.reddit.com/r/DnD/

https://www.reddit.com/r/40k/

