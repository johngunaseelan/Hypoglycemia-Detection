<H1 style="text-align: center;">Identifying Type 1 Diabetics With Severe Hypoglycemic Risks

</H1>

<H3>Project Overview</H3>

1.**Introduction**

  This tool is developed for the use of type 1 diabetics or physicians and other medical professionals who treat type 1 
diabetics to predict a patient's risk of hypoglycemia using machine learning models.

2.**Scope**

  To predict a patient's possibility of experiencing severe hypoglycemic events based on blood glucose levels and his/her
day to day activities

3.**Out Of Scope**

  Hypoglycemic unawareness, hyperglycemia or any other complications is beyond the scope of this project.



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
repository. A random forest model was created using this dataset to acheive the goal. A three fold cross validation was performed on 60/40 train test split to test the accuracy of the model.</P>

<P>The implementation was done using python's machine learning libraries like numpy, pandas, matplotlib, seaborn and scikit-learn.

<H3>Data Description</H3>

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
<a href="https://github.com/johngunaseelan/Hypoglycemia-Detection/blob/master/Code/Data-Wrangling.ipynb">link</a>

<ol>
<li>Delete rows that does not have a valid blood glucose value.</li>
<li>As the code feature is numerical for better readability add a new feature code_description which is a string representation
of the numerical feature code. The string representation is got from the data description provided in the dataset.</li>
<li>Alter date and time for invalid values by comparing with previous rows.</li>
</ol>

<H4>Exploratory Data Analysis</H4>

<P>Exploratory Dat Analysis was performed and following were the findings. Code and detailed comments can be seen in this 
<a href="https://github.com/johngunaseelan/Hypoglycemia-Detection/blob/master/Code/EDA.ipynb">link</a></P>

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
<a href="https://github.com/johngunaseelan/Hypoglycemia-Detection/blob/master/Code/Inferential-Statistics.ipynb">link
</a></P>

<ol>
<li>Irregular diet.</li>
<li>Snacks</li>
<li>NPH insulin</li>
<li>Median blood glucose level.</li>
<li>Irregular exercise.</li>
</ol>

<H4>Machine Learning</H4>

Random forest model seems to be the best algorithm for this problem.

<H4>Why Random Forest?</H4>

From EDA conclusions, we can infer that patients experience hypoglycemia for a number of independent reasons.

1) Being irregular with diet, exercise and snacking.
2) Strict control - People who are very conscious about their day to day activities also experience hypoglycemia as their efforts maintain optimal blood glucose levels sometimes lead to very low blood glucose levels which leads to hypoglycemic symptoms.
3) NPH insulin - People on NPH insulin are more prone to hypoglycemia.

We can see that there are three different sub populations within the hypoglycemic population. This makes random forest a best fit for the problem.

A random forest model was created using the following features.

<ol>
<li> Irregular diet</li>
<li> Median blood glucose level.</li>
<li> Number of NPH insulin shots per day</li>
<li> Number of readings per day. </li>
<li> Number of snack times per day</li>
</ol>

Code and detailed comments can be seen in this 
<a href="https://github.com/johngunaseelan/Hypoglycemia-Detection/blob/master/Code/Machine%20Learning.ipynb">link</a>

<H3>Testing</H3>

The dataset was divided into 60/40 Train test split. The model was able to predict with a maximum of 82% accuracy. The ROC-AOC
curve is displayed below.

![roc-aoc-image](https://github.com/johngunaseelan/Hypoglycemia-Detection/tree/DataWrangling/Meta/roc-aoc.png "")

<H3>Confusion Matrix</H3>

<table>
  <tr>
    <th>n=70</th>
    <th>Predicted Hypoglycemic</th>
    <th>Predicted Non-Hypoglycemic</th>
  </tr>
  <tr>
    <th>Actual Hypoglycemic</th>
    <td>Tn=11</td>
    <td>Fp=2</td>
  </tr>
  <tr>
    <th>Actual non-Hypoglycemic</th>
    <td>Fn=3</td>
    <td>Tp=12</td>
  </tr>
</table>

<H3>Conclusion</H3>

Hypoglycemia has always been the toughest problem for both the diabetic patients and the doctors. The doctors are helpless when it comes to glucose control as the lab reports can not convey the entire picture. With the latest advances in technology lab reports can now say the blood glucose levels at a certain point of time and the average blood glucose level for the past 3 months(Hba1c test). These reports can not say anything about a patient's risk of hypoglycemia or diabetic neuropathy(long term complications like kidney and eye damage). 

The patient's only option left is to check his glucose levels as frequent as possible. So a large data is generated. But, this data is left mostly unused and untouched. Medical science is yet to understand why few diabetic patients are more prone to hypoglycemia and diabetic neuropathy and other patients dont. Billions of dollors are spent every year on research and control of the disease. Even with millions of diabetics around the world it still does not know its causes or its cure. Can data science be the missing link to solve these riddles? I strongly believe so. 

Our study focuses on helping out the doctors and patients to better control the disease. In our study of seventy patients we have identified sub populations within the hypoglycemia prone diabetics. We have identified few day to day habits that are major causes. Below is our recommendations to the diabetics from our study.

1) Be regular in your day to day activities. Maintain a pattern with diet and exercise.
2) Snack less. Snacks are known to contain a lot of carbs. Lesser the snacks greater the control.
3) NPH insulin users can discuss with the physicians for alternate treatments.
4) A strict control may not be neccessary. blood glucose target levels can be slightly higher for diabetics than the normal population.

This model with 82% accuracy should be very helpful for physicians to identify at risk hypoglycemic patients and treat them better. Further studies are required in this area to help the patients and physicians.
