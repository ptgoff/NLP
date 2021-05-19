# NLP Proposal
Peter Goff

## Goal: Predict the impact of quarterly earning reports on stock behavior
In quarterly earning reports, company leadership shares perspectives on the company, their fundamentals, challenges, mission, direction, investments, and general fiscal health of the organization. Quarterly earning calls are (typically) recorded conference calls where leadership summarizes the earnings report and often engages questions from those outside the organization. This project will explore the features of earnings calls that coincide with increased earnings. <br>
The content and sentiment of the call both shape public receptivity and direct subsequent action on the part of investors. Thus, the two key features for this study will be topic affiliation and sentiment. Additional market-based and call-based measures will be integrated as well.

### Defining the target
The target outcome for this study is to identify stocks that have increased in value in the week following the quarterly earnings call. To temper against stochastic fluctuations, I will calculate each company's average stock price from the week prior to the call and compare this with the average stock price in the week following the call. This 7-day window may be tuned to be wider or narrower following EDA. An increase of five percent will be classified as a notable increase; anything less than this will be classified as not having a notable increase. This 5% threshold may also be tuned following EDA.

### Features
The features for this study will topic affiliation and sentiment. Topic affiliation will be determined via principal component analysis (pca) with [varimax rotation](https://pypi.org/project/advanced-pca/). Recent work has shown this to be a robust approach to topic modeling of [text data](https://arxiv.org/abs/2004.05387). Nonetheless, identifying a text with given topic does not provide any insight as to *how* that topic is being engaged. For example, one topic that may emerge from an analysis of earning calls may identify calls that engage recent legislation or policies. While this is interesting, it would be helpful to have some insight as to how the leadership sees the legislation or policies impacting the organization. <br>

[Sentiment analysis](https://codingandfun.com/company-earnings-sentiment-analysis-with-python/), which (typically) conveys binary good/bad sentiment of a text, has seen great popularity in analyzing text within the finance sector in recent years. Sentiment analysis can be seen as the yin to the topic modeling's yang; that is, sentiment analysis is entirely ignorant of the content of the text. Ideally, coupling topic modeling with sentiment analysis will temper the weaknesses of each approach. Interacting these features in a modeling context will allow us to identify changes in the target that are associated with a given topic when that topic is engaged in a positive or negative manner. <br>

It is possible that general market trends will cause a general increase or decrease in stock prices. Proportional increase across the market broadly (S&P 500) and the sector specifically will be included to temper this possibility. Other features for inclusion will be: trend data (linear slope of stock price leading into the call), shares available (float), and options trading metrics (calls, shorts/puts). 

### Defining the sample
One concern for this study is that the topic modeling will reveal valid yet uninformative topics. For example, a sample of random sample of stocks calls may produce topics that simply reflect the sector of the stock (e.g., health care, technology, utilities). To mitigate that possibility, I will select a sample of companies from within the same sector. 

### Data
Stock data will be gathered from [yfinance](https://medium.com/analytics-vidhya/trading-dashboard-with-yfinance-python-56fa471f881d) [API](https://pypi.org/project/yfinance/). Earnings call transcripts will be scraped from [Seeking Alpha](https://seekingalpha.com/earnings/earnings-call-transcripts). 

### Tools
Web scraping of transcript data will use the BeautifulSoup and Requests libraries
Preprocesing of transcripts will use textblob and nltk with 
Topic modeling will be conducted using 

### MVP 
Minimum viable product will be a classifcation model that predicts stocks which have increased in value following a quarterly earnings call. The model will be selected from a set of potential models using training, validate, and test data splits with any applicable hyper-parameters appropriately tuned to maximize predictve power and temper errors. Feature engineering will complement model selection and tunging. Appropriate visualizations and model application will be used to convey the practical import and power of the model.
