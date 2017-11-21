Problem statement
1. To recommend e-news articles to twitter users based on their interests and tweets posted by them in the past.
2. To find the credibility of twitter users on the basis of tweets posted by them.

In twitter, user can view news feed on their homepage which are according to who they follow. Moreover user can also view trending news. There are lots of lies being spread on Twitter, so finding uncredible users who tweet lies is an important task.
There is no certainty about the credibility of tweets. Because of the short size of tweet, the news content present is very low. Though there are trending topics in twitter, but we can improve the user experience by recommending news to the user based on his interests i.e. their tweets, tweets they retweet or make favorites.



Task 1 - User Credibility
Input :
- User Tweets
- User Profile Data
- News Articles

Description: The task is to evaluate how credible the user is. Credibility of a user composes of 2 parts: Tweets credibility and User’s profile credibility. 
1) To find tweets credibility -
    (A) Find if the tweet is a truth or not
    - For each tweet, find the modified jaccard similarity (in the denominator of jaccard don't take union of news summary and tweet, rather only consider tweet so as to consider only tweets length for finding similarity) between the summarized news articles and the tweet.
    - For each user, take the average of similarities of all the tweets corresponding to that particular user.
    (B) Use Tweets factors for a 3 points system. Points corresponding to each factor are - 
    - If there are many Retweets of the tweet, assign a point to it. Set a threshold for number of RTs, taken 75 here.
    - If there are many Favorites done on the tweet, assign a point to it. Set a threshold for number of FAVs, taken 75 here.
    - In twitter, since words limit is there. TinyURLs are used. These URL’s may also not be credible. So extract the full URL from TinyURLs used in each of the tweet and if there exists a corresponding full URL which opens, assign a point.

2) To find user’s profile credibility -
To find profile credibility a 7 points based method is used. Points corresponding to each factor are -
    - Verified Profile - 2 points
    - Find Followers/Following ratio and use a threshold. Here if ratio>0.8, assign 2 points to the user. If the ratio>0.4, assign 1 point to the user.
    - Linked to some other social networking site - 1 point
    - User has listed his website - 1 point
    - User has added his/her description - 1 pointe credible. So extract the full URL from TinyURLs used in each of the tweet and if there exists a corresponding full URL which opens, assign a point.

3) Hybrid Approach - 
    - Combine the above two above approaches. 
    - We get a 10 point system, 7 from user’s profile, 3 from tweets. Divide these total points for each user by 10.
    - Use the formula 0.75*Tweet_truth+0.25*points to find the total user credibility based on both the approaches. In the above formula ratios can be modified to give more weightage to one factor or the other.
    - Set thresholds to divide the credibility categories into 4 parts - [Highly Credible, Credible, Not Credible, Highly Uncredible]
    - Threshold intervals taken here are [0-0.20 , 0.20-0.40 , 0.40-0.65 , 0.65-1]
    - The results are saved in a file.



Task 2 - User Interest Profile
Input :
- User Tweets
- User Profile Data
- News Articles

Description: The task is to find the interests of a user. 
    - Take categories for news. Here, these are - sports, entertainment, health, lifestyle, politics, relationships, technology
    - Keep on appending keywords for all news articles crawled into files corresponding to their category.
    - For each tweet of a user, find its cosine similarity with the categorised documents.
    - For all the tweets of user, add the similarity values together corresponding to the category. So we get a list of user with his/her similarity with all the categories. 
    - This is done for all the users and the result is stored in a file user_profile.csv
    - Also, find the maximum similar category for each user and store the result in user_interest.csv
    -These files can then be used for recommending articles based on user interest.
