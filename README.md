<H1 style="text-align: center;">Identifying Type 1 Diabetics With Severe Hypoglycemic Risks

</H1>

<H3>Project Overview</H3>
<ol>
<li> Introduction</li>

<P>This tool is developed for the use of type 1 diabetics or physicians and other medical professionals who treat type 1 
diabetics to predict a patient's risk of hypoglycemia using machine learning models.</P>

'<li>Scope</li>

<P> To predict a patient's possibility of experiencing severe hypoglycemic events based on blood glucose levels and his/her
day to day activities</p>

<li>Out Of Scope</li>
<p>Hypoglycemic unawareness, hyperglycemia or any other complications is beyond the scope of this project.</p>

</ol>

<H3>Background</H3>

<P><B>Type 1 diabetes</B> is a chronic disease where patient's body no more produces enough insulin to regulate the blood glucose 
levels. This condition is treated by injecting actificial insulin into the body few times a day to maintain the body's blood 
glucose levels within the desired range. This treatment comes with side effects called hyperglycemia and hypoglycemia. 
<B>Hyperglycemia</B> is caused when lesser than required insulin is injected which causes the blood sugar levels to be above the 
desired range and <B>Hypoglycemia</B> is caused when more than required insulin is injected which causes the body's blood sugar 
levels to drop to sudden deadly lows which may cause coma or even death when not treated promptly.</P>

<P>While hyperglycemia is linked to long term complications in diabetics, hypoglycemia is a daily threat. Hypoglycemia is a 
result of day to day activities and are spontaneous and therefore can not be detected in advance. The medical professionals
rely on daily blood glucose levels and a patient's day to day habits to treat the patient.</P>

<P>Please go through <a href="https://www.webmd.com/diabetes/type-1-diabetes-guide/default.htm">this article</a> to understand 
the disease in depth.</P>

<P> This tool is developed primarily for the physicians and medical professionals to analyze a patient's possibility of
experiencing hypoglycemic complications. The tool analyzes a patient's daily blood glucose levels and day to day activities
to predict whether a patient is at rist to experience severe hypoglycemia.</P>

<H3>Design Of The Study</H3>

<P>The model uses the <a href="https://archive.ics.uci.edu/ml/datasets/diabetes">dataset</a> got from the UCI machine learning 
repository. A random forest model was created using this dataset to acheive the goal. A three fold cross validation was performed
on 60/40 train test split to test the accuracy of the model.</P>

<H3>DataSet</H3>

<p>The <a href="https://archive.ics.uci.edu/ml/datasets/diabetes">dataset</a> is a multivariate time series dataset.</p>

<P>The dataset contains blood glucose logs with the associated events of seventy patients for at least three weeks. The log 
for each patient is contained as a seperate file.</p> The dataset contain's the following features.

<H4>Features</H4>
<ul>
<li> Date - Date of the blood glucose level.</li>
<li> Time - Time of the blood glucose level.</li>
<li> Code - A number that represent's the event or activity during the blood glucose level collection. Example: before breakfast.</li>
<li> Blood Glucose level</li>
</ul>

A detailed information on the dataset can be found <a href="https://archive.ics.uci.edu/ml/datasets/diabetes">here.</a>

<H3>Procedure</H3>

<H4>Data Wrangling</H4>

The following steps were done to clean the data. Code and detailed comments can be seen in this 
<a href="http://localhost:8889/notebooks/Documents/GitHub/Hypoglycemia-Detection/Code/Data-Wrangling-II.ipynb">link</a>

<ol>
<li>Delete rows that does not have a valid blood glucose value.</li>
<li>As the code feature is numerical for better readability add a new feature code_description which is a string representation
of the numerical feature code. The string representation is got from the data description provided in the dataset.</li>
<li>Alter date and time for invalid values by comparing with previous rows.</li>
</ol>

<H4>Exploratory Data Analysis</H4>

<P>Exploratory Dat Analysis was performed and following were the findings. Code and detailed comments can be seen in this 
<a href="http://localhost:8889/notebooks/Documents/GitHub/Hypoglycemia-Detection/Code/EDA-III.ipynb">link</a></P>

<ol>
<li>The median blood glucose level for hypoglycemic population is slightly higher for non hypoglycemic population</li>
<li>The standard deviation of blood glucose level is slightly higher for the hypoglycemic population</li>
<li>The hypoglycemic population exercises more than the non-hypoglycemic population. This may imply that tight control may be one of the reasons for hypoglycemia.</li>
<li>The hypoglycemic population was significantly irregular in their day to day activities than their counterparts.</li>
<li>The hypoglycemic population snacked more than their counterparts.</li>
<li>The hypoglycemic population had significantly more blood glucose readings than their counterparts. This may suggest that strict control may be causing hypoglycemia in these patients.</li>
<li>The hypoglycemic population takes more insulin shots per day. This may suggest irregularities. </li>
<li>NPH insulin users have slightly higher chances of experiencing hypoglycemia than non users.</li>
<li>Most hypoglycemic events happen during the afternoon 12 noon and 6pm</li>
<li>The hypoglycemic population had significantly higher blood glucose levels post lunch on non hypoglycemic days than on hypoglycemic days</li>
</ol>

<H4>Inferential Statistics</H4>

<P>A correlation matrix was created using the most significant features that were got from EDA. Below is the most significant 
features as got from correlation matrix. This features will be used to create the machine learning models.</P>

<P>Code and detailed comments can be seen in this 
<a href="http://localhost:8889/notebooks/Documents/GitHub/Hypoglycemia-Detection/Code/Inferential-Statistics.ipynb">link
</a></P>

<ol>
<li>Irregular diet.</li>
<li>Snacks</li>
<li>NPH insulin</li>
<li>Median blood glucose level.</li>
<li>Irregular exercise.</li>
</ol>

<H4>Machine Learning</H4>

A random forest model was created using the following features.

<ol>
<li> Irregular diet</li>
<li> Median blood glucose level.</li>
<li> Number of NPH insulin shots per day</li>
<li> Number of readings per day. </li>
<li> Number of snack times per day</li>
</ol>

Code and detailed comments can be seen in this 
<a href="http://localhost:8889/notebooks/Documents/GitHub/Hypoglycemia-Detection/Code/Machine%20Learning-III.ipynb">link</a>

<H3>Testing</H3>

The dataset was divided into 60/40 Train test split. The model was able to predict with a maximum of 82% accuracy. The ROC-AOC
curve is displayed below.

![alt roc-aoc-image](https://github.com/johngunaseelan/Hypoglycemia-Detection/tree/DataWrangling/Meta/roc-aoc.png)

<H3>Conclusion</H3>

This model with 82% accuracy should be very helpful for physicians to identify at risk hypoglycemic patients. A further time
series model can be created in the future to identify if daily blood sugar levels have anything to do with hypoglycemia.
