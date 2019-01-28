# PUBG Finish Placement Prediction on Kaggle
<div class="markdown-converter__text--rendered"><p><img src="https://storage.googleapis.com/kaggle-media/competitions/PUBG/PUBG%20Inlay.jpg" alt="PUBG" width="350" style="float:right;"></p>

<p>So, where we droppin' boys and girls?</p>

<p>Battle Royale-style video games have taken the world by storm. 100 players are dropped onto an island empty-handed and must explore, scavenge, and eliminate other players until only one is left standing, all while the play zone continues to shrink. </p>

<p>PlayerUnknown's BattleGrounds (PUBG) has enjoyed massive popularity. With over 50 million copies sold, it's the fifth best selling game of all time, and has millions of active monthly players.  </p>

<p>The team at <a href="https://www.pubg.com" rel="nofollow">PUBG</a> has made official game data available for the public to explore and scavenge outside of "The Blue Circle." This competition is not an official or affiliated PUBG site - Kaggle collected data made possible through the <a href="https://developer.pubg.com" rel="nofollow">PUBG Developer API</a>.</p> 

<p>You are given over 65,000 games' worth of anonymized player data, split into training and testing sets, and asked to predict final placement from final in-game stats and initial player ratings. </p>

<p>What's the best strategy to win in PUBG? Should you sit in one spot and hide your way into victory, or do you need to be the top shot? Let's let the data do the talking!</p></div>


# Here's my approach:

<div class="text_cell_render border-box-sizing rendered_html">
<h4>First of all what is Gradient Boosting?<a class="anchor-link" href="#First-of-all-what-is-Gradient-Boosting?">¶</a>
</h4>
<h5>Credits for this part goes to Sunil Ray<a class="anchor-link" href="#Credits-for-this-part-goes-to-Sunil-Ray">¶</a>
</h5>
<p>Definition: The term ‘Boosting’ refers to a family of algorithms which converts weak learner to strong learners.</p>
<p>Let’s understand this definition in detail by solving a problem of spam email identification:</p>
<p>How would you classify an email as SPAM or not? Like everyone else, our initial approach would be to identify ‘spam’ and ‘not spam’ emails using following criteria. If:<br></p>
<p>-Email has only one image file (promotional image), It’s a SPAM<br>
-Email has only link(s), It’s a SPAM<br>
-Email body consist of sentence like “You won a prize money of $ xxxxxx”, It’s a SPAM<br>
-Email from our official domain “Analyticsvidhya.com” , Not a SPAM<br>
-Email from known source, Not a SPAM<br></p>
<p>Above, we’ve defined multiple rules to classify an email into ‘spam’ or ‘not spam’. But, do you think these rules individually are strong enough to successfully classify an email? No.<br></p>
<p>Individually, these rules are not powerful enough to classify an email into ‘spam’ or ‘not spam’. Therefore, these rules are called as weak learner.<br></p>
<p>To convert weak learner to strong learner, we’ll combine the prediction of each weak learner using methods like:
•   Using average/ weighted average<br>
•   Considering prediction has higher vote<br></p>
<p>For example:  Above, we have defined 5 weak learners. Out of these 5, 3 are voted as ‘SPAM’ and 2 are voted as ‘Not a SPAM’. In this case, by default, we’ll consider an email as SPAM because we have higher(3) vote for ‘SPAM’...<br>
For full blog post: <a href="https://www.analyticsvidhya.com/blog/2015/11/quick-introduction-boosting-algorithms-machine-learning/">https://www.analyticsvidhya.com/blog/2015/11/quick-introduction-boosting-algorithms-machine-learning/</a></p>
<h4>Introduction to Gradient Boost Algorithms<a class="anchor-link" href="#Introduction-to-Gradient-Boost-Algorithms">¶</a>
</h4>
<h5>Credits for this part goes to my fellow friend Sefik Ilkin Serengil<a class="anchor-link" href="#Credits-for-this-part-goes-to-my-fellow-friend-Sefik-Ilkin-Serengil">¶</a>
</h5>
<p>It is a fact that decision tree based machine learning algorithms dominate Kaggle competitions. More than half of the winning solutions have adopted XGBoost. Recently, Microsoft announced its gradient boosting framework LightGBM. Nowadays, it steals the spotlight in gradient boosting machines. Kagglers start to use LightGBM more than XGBoost. Even though XGBoost might have higher accuracy, LightGBM runs previously 10 times and currently 6 times faster than XGBoost. Moreover, there are tens of solutions standing atop a challenge podium...<br>
For full blog post: <a href="https://sefiks.com/2018/10/13/a-gentle-introduction-to-lightgbm-for-applied-machine-learning/">https://sefiks.com/2018/10/13/a-gentle-introduction-to-lightgbm-for-applied-machine-learning/</a></p>
<h4>Introduction to Gridsearch<a class="anchor-link" href="#Introduction-to-Gridsearch">¶</a>
</h4>
<p>It is in simple implementation of auto-hyperparameter tuning. scikit learn team integrated a GridsearchCV function inside of model_selection library of theirs. It exhaustively searches over specified parameter grid (multiple values for each hyperparameter) values for a given estimator.</p>
<p>GridSearchCV implements a “fit” and a “score” method on array of hyperparameters specified in grid params set. It also implements “predict”, “predict_proba”, “decision_function”, “transform” and “inverse_transform” if they are implemented in the estimator used and returns back best_score, best_parameters that fits your data for the training. So we leave trial-error part to scikit learn.</p>
<p>Usage is simply:</p>
<p>from sklearn import svm, datasets<br>
from sklearn.model_selection import GridSearchCV<br>
iris = datasets.load_iris()<br>
parameters = {'kernel':('linear', 'rbf'), 'C':[1, 10]}<br>
svc = svm.SVC(gamma="scale")<br>
clf = GridSearchCV(svc, parameters, cv=5)<br>
clf.fit(iris.data, iris.target)<br>
sorted(clf.cv<em>results</em>.keys())</p>

</div>
