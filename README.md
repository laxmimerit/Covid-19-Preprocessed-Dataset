# Covid-19-Preprocessed-Dataset
Latest Covid-19 Dataset

Coronavirus disease 2019 (COVID-19) time series listing confirmed cases, reported deaths and reported recoveries. Data is disaggregated by country (and sometimes subregion). Coronavirus disease (COVID-19) is caused by the [Severe acute respiratory syndrome Coronavirus 2 (SARS-CoV-2)][sars2] and has had a worldwide effect. On March 11 2020, the World Health Organization (WHO) declared it a pandemic, pointing to the over 118,000 cases of the coronavirus illness in over 110 countries and territories around the world at the time.

[covid]: https://en.wikipedia.org/wiki/Coronavirus_disease_2019
[sars2]: https://en.wikipedia.org/wiki/Severe_acute_respiratory_syndrome_coronavirus_2

This dataset includes time series data tracking the number of people affected by COVID-19 worldwide, including:

* confirmed tested cases of Coronavirus infection
* the number of people who have reportedly died while sick with Coronavirus
* the number of people who have reportedly recovered from it

# Sample Code

This is sample code by using you can get started working with this dataset.

git remote add origin git@github.com:laxmimerit/Covid-19-Preprocessed-Dataset.git


echo "running covid-19 data upload project"
ls
/home/ubuntu/anaconda3/bin/python upload.py

```
# import
# imports
import plotly.express as px
import plotly.graph_objects as go
import plotly.figure_factory as ff
from plotly.subplots import make_subplots

import folium
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

import math
import random
from datetime import timedelta
import warnings
warnings.filterwarnings('ignore')

#color pallette
cnf = '#393e46'
dth = '#ff2e63'
rec = '#21bf73'
act = '#fe9801'
```

Let's code
```
# load the dataset
df = pd.read_csv('Covid-19-Preprocessed-Dataset/preprocessed/covid_19_data_cleaned.csv', parse_dates=['Date'])

country_daywise = pd.read_csv('Covid-19-Preprocessed-Dataset/preprocessed/country_daywise.csv', parse_dates=['Date'])
countywise = pd.read_csv('Covid-19-Preprocessed-Dataset/preprocessed/countrywise.csv')
daywise = pd.read_csv('Covid-19-Preprocessed-Dataset/preprocessed/daywise.csv', parse_dates=['Date'])

# fill NA
df['Province/State'] = df['Province/State'].fillna("")
# grouping by date
confirmed = df.groupby('Date').sum()['Confirmed'].reset_index()
recovered = df.groupby('Date').sum()['Recovered'].reset_index()
deaths = df.groupby('Date').sum()['Deaths'].reset_index()


# See your first plot
fig = go.Figure()
fig.add_trace(go.Scatter(x = confirmed['Date'], y = confirmed['Confirmed'], mode = 'lines+markers', name = 'Confirmed', line = dict(color = "Orange", width = 2)))
fig.add_trace(go.Scatter(x = recovered['Date'], y = recovered['Recovered'], mode = 'lines+markers', name = 'Recovered', line = dict(color = "Green", width = 2)))
fig.add_trace(go.Scatter(x = deaths['Date'], y = deaths['Deaths'], mode = 'lines+markers', name = 'Deaths', line = dict(color = "Red", width = 2)))
fig.update_layout(title = 'Worldwide Covid-19 Cases', xaxis_tickfont_size = 14, yaxis = dict(title = 'Number of Cases'))

fig.show()
```

## Data

Data is in CSV format and updated daily. It is sourced from [this upstream repository](https://github.com/CSSEGISandData/COVID-19) maintained by the amazing team at [Johns Hopkins University Center for Systems Science and Engineering](https://systems.jhu.edu/) (CSSE) who have been doing a great public service from an early point by collating data from around the world.

### Sources

The upstream dataset currently lists the following upstream datasources:

- World Health Organization (WHO): https://www.who.int/
- DXY.cn. Pneumonia. 2020. http://3g.dxy.cn/newh5/view/pneumonia
- BNO News: https://bnonews.com/index.php/2020/02/the-latest-coronavirus-cases/
- National Health Commission of the People’s Republic of China (NHC): http://www.nhc.gov.cn/xcs/yqtb/list_gzbd.shtml
- China CDC (CCDC): http://weekly.chinacdc.cn/news/TrackingtheEpidemic.htm
- Hong Kong Department of Health: https://www.chp.gov.hk/en/features/102465.html
- Macau Government: https://www.ssm.gov.mo/portal/
- Taiwan CDC: https://sites.google.com/cdc.gov.tw/2019ncov/taiwan?authuser=0
- US CDC: https://www.cdc.gov/coronavirus/2019-ncov/index.html
- Government of Canada: https://www.canada.ca/en/public-health/services/diseases/coronavirus.html
- Australia Government Department of Health: https://www.health.gov.au/news/coronavirus-update-at-a-glance
- European Centre for Disease Prevention and Control (ECDC): https://www.ecdc.europa.eu/en/geographical-distribution-2019-ncov-cases
- Ministry of Health Singapore (MOH): https://www.moh.gov.sg/covid-19
- Italy Ministry of Health: http://www.salute.gov.it/nuovocoronavirus


### Note
Hi,
Recently, some of the countries have stopped reporting Covid data and it is also found discrepancies in data if taken from multiple sources. Data reported till July 2020 is quite accurate so we will only explore from Jan 2020 to July 2020.

Ref.

https://covidtracking.com/about-data/faq#why-have-you-stopped-reporting-national-recoveries

https://github.com/CSSEGISandData/COVID-19/issues/3464

https://github.com/CSSEGISandData/COVID-19/issues

1. Active Cases are calculated based on recoveries so this will not be also correct
2. Anything that requires recoveries in the calculation isn't 100% correct, like deaths/100recoveries, etc.

Here is some article to understand it

https://www.dallasnews.com/news/public-health/2020/05/19/why-arent-coronavirus-recoveries-always-reported/

https://abc11.com/nc-coronavirus-recovery-cases-update/6127051/


Most of these reports are based on the US but mostly it is true for the rest of the world.


