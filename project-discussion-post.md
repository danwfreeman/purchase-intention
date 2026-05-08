**Final Project Discussion - Online Shoppers Purchasing Intention Dataset**

Dataset main page: [here](https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset)

Dataset zip file: [here](https://archive.ics.uci.edu/static/public/468/online+shoppers+purchasing+intention+dataset.zip)


The dataset is from the *UCI Machine Learning Repository*.  The data models user behavior on a popular e-commerce site to predict the intent to make a purchase.

Note: The feature metrics relate to user behavior, such as time on a page, page type visited, time of year (special events), and bounce and exit rates.  We do not focus on page load performance, which can greatly persuade a purchase decision.


**Learning Question:**
- The question we are trying to solve is: **will a session result in a purchase.**
- This information is valuable because it can reveal which parts of the user journey on the e-commerce site add friction to the user's experience, thus causing undesirable behavior (high bounce/exit rates or no purchase).
- The strength of this data is that it models user behavior, but the weakness is that it leaves out one of the most important features for converting sessions: page load performance metrics.

**Dataset Details:**

- Contains feature vectors from 12,300 user sessions
- Each session belongs to a different user over a 1-year period, which helps avoid behavioral bias toward events, periods, or a specific user profile.
- The target variable is 'Revenue' and is labeled as a boolean (true/false), making the dataset appropriate for a supervised classification model.

**Model Selection:**

- The model is a classification model because the target variable 'Revenue' is binary (purchased or not purchased).
- There are a number of categorical features that will be converted using One Hot Encoding (_Month, OperatingSystems, Browser, Region, TrafficType, and VisitorType_)
- The other features are continuous and will need to be scaled so that models (specifically for Logistic Regression) do not give too much weight to larger values (_page counts, page durations, bounce rate, exit rate, page value, and special day score_). For example, a duration of ~1500 compared to a bounce rate of ~0.05 would show large discrepancies.

_Logistic Regression_ will provide a logical choice for a baseline model.  It works well for this binary classification model.  It can show which features are associated with a higher/lower probability of a purchase.

_Decision Trees_ will be interesting to compare with Logistic Regression, a decision tree can show how feature combinations result in a purchase or non-purchase.  Seeing this visually in a tree diagram will make it easy to interpret.

Since we're using Decision Trees, we should go a step further and run the data through a _Random Forest_.  This will be beneficial by reducing overfitting.  Some relationships may be complex resulting in the model learning 'too well' and thus overfitting.

_Neural Networks_ perform better with a very large dataset, and with only ~12k rows, I expect the simpler models listed above to be more reliable for this project.

Model performance will be evaluated using a confusion matrix, accuracy, precision, recall, and F1-score. Since purchases may be less common than non-purchases, I will not rely only on accuracy. I will likely prioritize F1-score because it balances precision and recall.

**Data Leakage:**
- The feature "PageValues" is a 'weighted score' and is derived once the user's session has converted, therefore it is a strong candidate for data leakage. The models should be run with and without this feature and the accuracy, precision, recall, and F1-score should be compared.

**Appendix - Feature Glossary:**
- *Administrative*: The number of administrative-type pages visited during the session, such as account, login, order status, or help-related pages.
- *Administrative Duration*: The total amount of time the visitor spent on administrative pages during the session.
- *Informational*: The number of informational pages visited during the session, such as policy, company information, shipping information, or general content pages.
- *Informational Duration*: The total amount of time the visitor spent on informational pages during the session.
- *Product Related*: The number of product-related pages visited during the session. This includes pages where the visitor is browsing or viewing products.
- *Product Related Duration*: The total amount of time the visitor spent on product-related pages during the session.
- *Bounce Rate*: A Google Analytics metric representing the percentage of visitors who entered the site from a page and left without triggering another request during that session. A higher bounce rate may indicate lower engagement.
- *Exit Rate*: A Google Analytics metric representing the percentage of pageviews where a specific page was the last page viewed in the session. A higher exit rate may indicate that users are leaving the site from that page.
- *Page Value*: The average value of a page based on whether users who visited that page later completed an e-commerce transaction. This feature may be highly predictive, but it should be checked for possible data leakage.
- *Special Day*: A value indicating how close the session date is to a special shopping-related day, such as Mother’s Day or Valentine’s Day. Values closer to 1 indicate the session occurred very close to a special day.
- *Month*: The month of the year in which the session occurred. This can capture seasonal shopping patterns.
- *Operating System*: A categorical feature representing the visitor’s operating system. This may help capture differences in user behavior or technical experience across platforms.
- *Browser*: A categorical feature representing the browser used by the visitor. Browser type may be related to technical performance, compatibility, or user behavior.
- *Region*: A categorical feature representing the visitor’s geographic region. This may help capture location-based differences in shopping behavior.
- *Traffic Type*: A categorical feature representing how the visitor arrived at the site, such as direct traffic, search, referral, or other traffic sources.
- *Visitor Type*: A categorical feature indicating whether the visitor is a new visitor, returning visitor, or another visitor type. Returning visitors may be more likely to purchase than new visitors.
- *Weekend*: A Boolean feature indicating whether the session occurred on a weekend. Shopping behavior may differ between weekdays and weekends.
- *Revenue*: The target variable. This Boolean value indicates whether the session resulted in a transaction. For the model, this would be converted into a binary classification label, such as 1 = purchase and 0 = no purchase.


