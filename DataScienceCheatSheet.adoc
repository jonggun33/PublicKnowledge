# Data Science Cheatsheet - Python
:sectnums:
//:toc: left
:toclevels: 2

## Vanilla Python
[source, python]
dict(zip(list1, list2)) #create a dict from two lists
#string formatting
d_ = [f'd_{i:02}' for i in range(80)]

## Jupyter Notebook
[source, bash]
pd.set_option('display.max_rows', 10)
%reset -f #clears all variables
Shift + Tab : Show Tooltip
p: Show Command Pallette
y: Code, m: Markdown
M: Merge selected cells
o: output toggle, O: output scrolling
clear_ouptput(wait=True)

## Numpy
[source, python]
#apply operation on elements of a series
np.round(p, decimals=4)  
np.sqrt(df)  
#flattening an array of arrays
np.concatenate([[1], [2,3], [1,4,5]]) #OR
sr.values.flatten()  
#padding
a=ones(3); np.pad(a, (0, 3), 'constant', constant_values=2)
np.pad(group.angle.values, (0, max(0, 80-size)) )[0:80]
####vectorizer: 정의된 함수를 ndarray의 각 element에서 쓸수 있게 함.
filter = np.vectorize(lambda x: x if abs(x)>1.0 else 0.0)
filter(lr.coef_)
#tiling
a = np.array([1,2,3,4])
np.tile(a, (3,1))
a = np.ones((3,2)); b = np.ones((1,2))
a+b == a + np.tile(b.(3,1))
np.skey(arr)
np.log(arr)

## Pandas
### DataFrame creation.. plus alpha
[source, python]
pd.read_csv('abc.csv', sep='\t', index_col = 'abc', encoding='CP949', headers = None)  
df = sr.to_frame()
pd.set_option('display.max_row', None)  
df = DataFrame(randn(7, 7), columns= list('abcdefg'))  
q1 = 강원시작.quantile(0.25);   median = 강원시작.median()  
data.previous.value_counts()  
df.astype('bool').sum(axis=1)

### Indexing
[source, python]
#set_index
df.set_index(['date', '시작']) #인덱스 컬럼을 변경함  
#reset_index(): 기존의 인덱스를 버리고, 단순 인덱스로 다시 돌아감. 단순인덱스는 다시 순서대로 매김
df.reset_index( drop=True)  # index를 다시 매김, sort등 후 index에 일련번호 부여. drop: 기존 index 대체
충청강원 = 충청강원.reset_index(level='시작', drop=True)   # index를 다 없애지 않고 'level' 열의 인덱스만 없앰
#reindex(): index 값을 주어진 ㅣ값들로 재지정한다. 보간할 수도 있고, 일부만 남길 수도 있음
highway.reindex(index=['강원'], level='시작').stack()  # 검색을 수행함  
over50_mean = groups.mean().reindex(over50.index)  
yearly.reindex(index=np.arange(1908, 2001), fill_value=0) #모든 연도의 행들을 만듬

### Search/Sorting
[source, python]
df.iloc[0] #search by location; df.loc[0] #search by index;
df.sort_values(['col1', 'col2'], ascending=False, inplace =True, na_position='first')  
df['amount'].rank(method= 'min', ascending=False)  
mask2015 =( (data['AB'] > 400) & (data['yearID'] == 2015) )  #Use & instead of AND 
data5 = data[mask2015] ;  data6 = data[mask2016]  
len(set(data6.playerID).intersection(set(data5.playerID)) )  
krx[krx.Name.isin( monitoring)]   
data.education = np.where(data.education.str.contains( 'basic'), 'Basic', data.education)  
df.sort_index()
train['gu'] = train['address'].str.findall('\w+-gu').str[0]
    
### fillna() rename() replace() dropna()
[source, python]
df.rename(columns = {'a':'A', 'b':'B'})  
df['column1'].replace({'a':'A'})  
df.drop(['Xgrp'], axis = 1)  
df.dropna()  
df.drop_duplicate()
df.fillna(ffill)  
#Nan 값을 median으로 대체하는 방법  
df.dropna(how='any', subset=['a', 'b'])

### Reshaping
[source, python]
iris.reset_index().melt(id_vars = ['index'] , value_vars=['sepal_length', 'sepal_width'])  # col 들을 variable 컬럼에 모으고 value 컬럼에 값들을 넣어 줌  
#df.reshape()
boston.data[2].shape # (13,)
boston.data[2].reshape(1,-1).shape #(1, 13). -1 is for autosetting according to the previous parameter 
melted.pivot(index='index', columns= 'variable')  # melt의 반대 operation  
#stacking: 세로로 길어짐.. melting을 수행하는데, column 하나를 multi index의 젤 안쪽으로 가져 감  
iris.groupby(['big', 'species']).petal_width.count().unstack()  
heat = pd.crosstab(data['AgeClass'], data['Positive']).apply(lambda x: x/x.sum(), axis =1)  
  
### map/apply/applymap
[source, python]
df['col1'].map(lambda x: x**2)  
df['col'].apply(mean)  
df.applymap(lambda x: x**2)  
data.loc[:, 'arctan_1':'arctan_79'].applymap(lambda x: x !=0).sum().sum()  

### groupby
[source, python]
요일추출 = lambda 날짜: 날짜.weekday() ;  월추출 = lambda 날짜: 날짜.month  
월별_요일별_평균 = 충청강원.groupby([월추출, 요일추출]).mean().unstack()  
월별_요일별_평균.columns = list('월화수목금토일')  
movers = data.groupby('playerID').teamID.nunique() #nunique: count distinct values  
data.groupby('playerID').teamID.apply(lambda x: len(x.unique() ) )  
data['PrevRating'] = data.groupby('ClothingID')['Rating'].shift(1)  #아래 방향으로 1 shift.  
df.groupby('a').agg([np.sum,  sp.size])
df.groupby('a')['a'].value_counts()
    
### Partition
[source, python]
df.groupby('seller_name')['close_date].rank(method='first')
  
### merge & concat
[source, python]
pd.merge(df1, df2) #using the common column  
pd.merge(df1, df2, on='col1', how='left/inner', left_index=True)  
fivesix = pd.merge(data5, data6, on='playerID', how='inner')  
pd.merge(df1, df2, left_index=True, right_index = True)  #Index로 Join 하는 경우  
pd.concat([df1, df2], axis = 1) #columns를 합침  
  
### Series str/dt
[source, python]
df['age_gender'].str.split().str[0]  
pd.to_datetime(df['Date'], format='%m/%d/%Y').dt.year    # dt works on a series  

## statistics
### Normality
[source, python]
df.hist()
from statsmodels.graphics.gofplots import qqplot
qqplot(data, line='s')
from scipy.stats import shapiro
stat, p = shapiro(data) #p>alpha: looks Normal
#Box-Cox Transformation
boxcox = sp.stats.boxcox(df['Passengers'])
####Jarque Bera
sp.stats.jarque_bera(v).pvalue

### 동일평균테스트
[source, python]
from scipy.stats import ttest_ind, ttest_rel  
ttest_ind(df1, df2, equal_var = False)  
#(t-value, p-value): p-value: 평균이 같다고 했을 때, 이러한 관측 결과가 나올 확률, 유의수준(0.05) 보다 낮으면,
# 이런 관측이 나오기 어렵다고 보고 평균이 같다는 가서을 기각함
ttest_ind(list(groups)[0][1], list(groups)[1][1])  
from scipy.stats import f_oneway ;  f_oneway(df1, df2, df3)  
G123 = [df1, df2, df3]; f_oneway(*G123);  
#######################
groups = base_table.groupby('Doors').Price  
f_oneway(*[one[1] for one in list(groups)])  
######################
#chi2_contingency  
#####################
from statsmodels.stats.multicomp import pairwise_tukeyhsd  
posthoc = pairwise_tukeyhsd(df['col1'], df['col2'], alpha =0.05)  

### Correlation, Covariance
[source, python]
from scipy.stats import pearson;   pearson(sr1, sr2)  
corr = df.corr(method = 'pearson')  # rank correlation = spearman  
pltl.matshow(corr.Target)  
df.cov()
  
## Time Series Analysis
### Basic
[source, python]
year_index = pd.period_range(start='1908', end='2000', freq='Y') #OR reindex()

### Moving Averages
[source, python]
#simple moving average
df.Count.rolling(5).mean().shift(1) # mean of the 5 previous values including the curren #shift(1) if you want exclude the current
df.Count.rolling(5, min_periods=1).mena() #1개만 있어도 그걸로 mean()
#Cumulative Moving Average
df.Count.expanding().mean() #mean of all the previous values including the current
#weighted moving average
weights = [0.25, 0.25, 0.5]
wma = df.Count.rolling(5).apply(lambda x: np.dot(x, weights)).mean()
#Exponential Moving Average
ema = df.Count.ewm(alpha=0.3, adjust=False).mean().shift(1)

### Autocorrelation
[source, python]
from pandas.plotting import lag_plot
from pandas.plotting import autocorrelation_plot
from statsmodels.graphics.tsaplots import plot_acf
plot_acf(series, lags = 31) #specifies maximum lag
from statsmodels.tsa.ar_model import AutoReg
model AutoReg(train, lags=29)
model.fit()

### Holt's Winters Seasonal
[source, python]
from statsmodels.tsa.api import ExponentialSmoothing
model = ExponentialSmoothing(endog = timeseriesdata, trend='add', seasonal='add, seasonal_periods=12).fit()
model.forecast(12)

### Stationary
[source, python]
#NO trend, periodity
from statsmodels.tsa.stattools import adfuller #Augmented Dickey-Fuller Test
result = adfuller(df.Count)
print('ADF Statistic: %f' % result[0])
print('p-value: %f' % result[1]) #<0.05: stationary 하면서 이렇게 될 가능성은 0.05 이하임
print('Critical Values:')
for key, value in result[4].items():
    print('\t%s: %.3f' % (key, value))
result = adfuller(df.Count.diff()) #1차 차분으로 d=1 결정

### ARIMA (Auto-Regressive Integrated Moving Average)
[source, python]
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf #(Partial) Auto Correlation
plot_acf(diff_1); plot_pacf(diff_1)
from statsmodels.tsa.arima_model import ARIMA

## Preprocessing
[source, python]
from sklearn.model_selection import train_test_split  
X_train, X_test, y_train, y_test = train_test_split(housing.drop(['Target'], axis = 1, test_size=0.3, stratify = 'col1'), housing['Target'] )  
df.get_dummies('teamID');  pd.get_dummies(df)  
from sklearn.preprocessing import OneHotEncoder  
en = OneHotEncoder().fit_transform(data[['playerID', 'teamID']] )  

### Normalization
[source, python]
df[cols]/df[cols].max(axis=0)
from sklearn.preprocessing import MinMaxScaler, StandardScaler  
X = MinMaxScaler().fit_transform(df)  

### PCA
[source, python]
from sklearn.decompositions import PCA ; decomposition = PCA(n_components = 15)  
decomposition.fit_transfrom(housing.drop(['Target'], axis = 1) )  
decomposition.explained_variance_ratio_.sum()  
decomposition.components_  
pca(X)@pca.components_ +X.mean(axis = 0) # 행 백터를 2차 행렬과 더하면 np.tile을 수행해서 하는 것과 동일한 효과

### SVD
[source, python]
U, Sigma, Vt = np.linalg.svd(A)
from sklearn.utils.extmath import randomize_svd
U, Sigma, Vt = randomized_svd(A, n_components =15)
from scipy.sparse.linalg import svds
U, Sigma, Vt = svds(A, k=15)
from sklearn.decomposition import TruncatedSVD
svd = TruncatedSVD(15)
svd.fit(A); 
Sigma = svd.singular_ 
svd.transform(A) # == np.dot(U, np.diag(Sigma) ) 
Vt == svd.components_
A = np.dot(np.dot(U, np.diag(Sigma) ), Vt)
  
### Under-Sampling
[source, python]
#w적은 클래스의 수만큼 상대 클래스 수도 under-sampling 하여 학습에 사용함 - 학습개선됨. 

### Over-Sampling
[source, python]
SMOTE:you should over sample only after choosing the train dataset    
X = data_final.loc[:, data_final.columns != 'y']  
y = data_final.loc[:, data_final.columns == 'y']. 
from imblearn.over_sampling import SMOTE. 
os = SMOTE(random_state=0)  
from sklearn.model_selection import train_test_split  
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=0)  
  
### Feature Selection
[source, python]
from sklearn.feature_selection import RFE #Recursive Feature Elimination  
rfe = RFE(LogisticRegression(), n_features_to_select=10 )  
rfe.fit(X_train, y_train)  
rfe.ranking_ ; rfe.support_ ;  rfe.predict(X_test)  

## Model Evaluation
### Metrics
[source, python]
from sklearn.metrics import roc_curve, roc_auc_score   
lr_probs = model.predict_log_proba(X_test)  
roc_auc_score(y_test, lr_probs)  
ns_fpr, ns_tpr, ns_threshold = roc_curve(y_test, ns_probs)  
from sklearn.metrics import confusion_matrix, accuracy_score  
confusion_matrix(y_true=y_test, y_pred=model.predict(X_test))  
accuracy_score(y_true=y_test, y_pred=model.predict(X_test))  
from sklearn.metrics import classification_report   
classification_report(y_true=y_test, y_pred=model.predict(X_test  
from sklearn.metrics import f1_score  
f1_score(y_true=y_test, y_pred=model.predict(X_test))  
from sklearn.metrics import plot_confusion_matrix, plot_precision_recall_curve, plot_roc_curve  
model.score(X_test, y_test) #mean accuracy  
import statsmodels.api as sm  
from statsmodels.sandbox.regression.predstd import wls_prediction_std  
X = sm.add_constant(df.drop(columns=['ID', 'none_high_d', 'cdiff']))  
y = df.cdiff   
model = sm.Logit(y, X).fit()  
model.summary2()  
#RMSE
from sklearn.metrics import mean_squared_error
rmse = mean_squared_error(real, predicted, squared = False)
from sklearn.metrics import mean_absolute_error
  
  
### Cross Validation
[source, python]
from sklearn.model_selection import KFold  
from sklearn.model_selection import cross_val_score  
model = LogisticRegression(solver ='lbfgs', C=1)  
cv = KFold(n_splits=10, random_state=1, shuffle=True)  
cross_val_score(model, X, y, scoring='accuracy', cv=cv)  
 
### Model Selection - Grid Search
[source, python]
from scipy.stats import loguniform  
space = dict()  
space['solver'] = ['newton-cg', 'lbfgs', 'liblinear']  
space['penalty'] = ['none', 'l1', 'l2', 'elasticnet']  
space['C'] = loguniform(1e-5, 100)  
from sklearn.model_selection import RandomizedSearchCV  
search = RandomizedSearchCV(model, space, n_iter = 2, scoring='accuracy',n_jobs = -1, cv=cv, random_state=1)  
result = search.fit(X, y)  
result.best_estimator_; result.predict(X_test); result.best_score_  

### Pipeline
[source, python]
from sklearn.pipeline import Pipeline
steps = []  
steps.append(('standardize', StandardScaler()))  
steps.append(('lr', LogisticRegression()))  
model = Pipeline(steps)  
kfold = KFold(n_splits=10, random_state=1)  
results = cross_val_score(model, X, y, cv=kfold)  

## plotting
### pyplot
[source, python]
plt.boxplot(G123)  
pd.plotting.scatter_matrix(housing, S=60, alpha =0.8, hist_kwds={'bins':30} )
corr = housing.corr(method='pearson')  
pearson = corr['Target']  
plt.matshow(corr)  
table = pd.crosstab(data.marital, data.y)
print(table)  
table.sum(0)  
table = table.div(table.sum(1).astype(float), axis=0)  
table.plot(kind = 'bar', stacked=True)  
df.y.hist() #plot with df

### Seaborn
[source, python]
import seaborn as sns
fig, axes = plt.subplots(1,5)
fig.set_size_inches(15, 5)
sns.distplot(PromoA, ax=axes[0])
plt.show()

### graphing
[source, python]
import networkx as nx

## Clustering
### K-means
[source, python]
from sklearn.cluster import KMeans  
군집예측 = KMeans(n_clusters=3, random_state - 1234).fit_predict(X)  
군집예측.fit_predict(df)  
from sklearn.metrics import silhouette_score
silhoutte_score(test_scaled, test_cluster)
  
### Mean-Shift Clustering


## Regression
### OLS (Ordinary Least Square)
[source, python]
import statsmodel.api as sm
X = sm.add_constant(X)
model = sm.OLS(y,X)
result = model.fit()
result.summary()

### Linear Regression
[source, python]
from sklearn.linear_model import LinearRegression  
model = LinearRegression(fit_intercept = True #default# ).fit(X_train, y_train)  
model.coef_  
model.score(X_train, y_train)  
y_pred = model.predict(X_test)  
a = {'col1':[4], 'col2':[3]}; one = pd.DataFrame(a); model.predict(one);  
  
### Ridge Lasso Regression
[source, python]
from sklearn.linear_model import Ridge, Lasso.   
clf = Ridge(alpha=1.0); clf = Lasso(alpha = 1.0);  
clf.fit(X, y)  
  
## Classification
### Logistic Regression
[source, python]
from sklearn.linear_model import LogisticRegression  
lr = LogisticRegression()  
lr.fit(X, y)  
np.exp(lr.coef) #Odds Ratio  
logi.score(X, y)  

### Decision Tree
[source, python]
from sklearn.tree import DecisionTreeClassifier  
DecisionTreeClassifier.fit(X, y)  

### KNN
[source, python]
from sklearn.neighbors import KNeighborsClassifier
knn = KneighborsClasifier(n_neighbors=3)
knn.fit(Xtrain, ytrain)

### Bayesian

### Support Vector Machine
[source, python]
from sklearn.pipeline import make_pipeline  
from sklearn.preprocessing import StandardScaler  
from sklearn.svm import SVC  
clf = make_pipeline(StandardScaler(), SVC(gamma='auto'))  
clf.fit(X, y)  

### Ensemble - Random Forest
[source, python]
from sklearn.ensemble import BaggingClassifier  
from sklearn.neighbors import KNeighborsClassifier  
bagging = BaggingClassifier(KNeighborsClassifier(),max_samples=0.5, max_features=0.5)  
from sklearn.ensemble import RandomForestClassifier  
clf = RandomForestClassifier(n_estimators=10)  

## association
[source, python]
from mlxtend.frequent_patterns import apriori, association_rules  
print('Support: ', DramaRomance/AllGenre)  
print('Confidence D->R: ', DramaRomance/Drama)  
lift = confidence/support  
freq = apriori(df, min_support=0.001, use_colnames = True)  
assoc = association_rules(freq, metric='confidence', min_threshold = 0.01)  
assoc[assoc.antecedents == {'Animation'}]  

## Recommendation
[source, python]
from sklearn.metrics.pairwise import cosine_similarity
from sklearn.feature_extraction.text import CountVectorizer
genre_cv = cv.transform(df.genres)
similarity = cosine_similarity(genre_cv, genre_cv)
np.argsort(similarity)
###implicit
###surprise

## NLP
### Bag Of Words
[source, python]
from sklearn.feature_extraction.text import CountVectorizer
cv = CountVectrizer();   cv.fit(X_train); X_train_cv = cv.transform(X_train) 
#Term Frequency - Inverse Document Frequency
from sklearn.feature_extraction.text import TfidfVectorizer
tv = TfidVectorizer(stop_words='english', ngram_range=(1,2), max_features=300, max_df = 0.5)
transformed = tv.fit(X_train).transform(X_train)
transformed.vocabulary_; transformed.toarray();
#############
doc2vec

### KOLNPY
[source, python]
from konlpy.tag import Kkma, Okt
okt = Okt(); okt.morphs()

  
