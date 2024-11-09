---
layout: post
title:  "How to Evaluate College Volleyball Players"
author: Shaelyn Eldrege
description: This article will talk about getting 
image: /assets/images/volleyballs.jpeg
display_image: True
---

## Introduction

There is so much data in sports. However, it can be hard to find and hard to get information out of it once you do find it. One of the biggest data sets out there comes from the collegiate level of competition. We will be exploring the ethics of how to get this information, how to webscrap it, and how to get some information out of it. We are looking at data on volleyball from the big 10 conference in 2023.

## Ethics of Webscrapping

Before webscrapping any website you should check the robots.txt file. This can be found on almost any website, all you have to do is type in the **url/robots.txt**. robots.txt files tell each type of bot what part of the website they are allowed to scrap. These are some examples of robots.txt files:

<img src="{{site.url}}/{{site.baseurl}}/assets/images/robots-txt.jpg" alt="" style="width:300px;"/>

These files show different bots and what they are allowed to scrap and disallowed scrap by each type of bot. For the general user you need to look at the bot file indicated with an astrix (*). Along with which parts of the website the file also can have some restrictions on how often you can make requests to a website, show in the 'Crawl-delay:'. Some websites also have restrictions on the hours that you can webscrap. You can find more information on webscrapping <a href="https://www.zenrows.com/blog/robots-txt-web-scraping#robots-txt-web-scraping" target="_blank">here</a>.

## Webscrapping

For this example we will be looking at the website for the Big 10 Conference volleyball teams. Before we get started we need to install all of the necessary packages to preform the webscrapping.

```
pip install pandas
pip install selenium
pip install webdriver-manager
pip install beautifulsoup4

```
Next the packages need to be imported for use. The following code chunk will can be used to get all the appropriate things from each package.

```
import pandas as pd
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from bs4 import BeautifulSoup
```

 We will look at all the volleyball players from the year 2023. This is the type of table we will be scrapping from.

<img src="{{site.url}}/{{site.baseurl}}/assets/images/big10table.jpg" alt="" style="width:300px;"/>

First, we need to set up the driver we will be scrapping from. We do this with the following code.

```
url = 'https://bigten.org/wvb/stats/'
driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
driver.get(url)
```

 This website is special because it doesn't change the url when the year changes for the table. The default for the website is 2024, but we want to scrap the year 2023 to be change the year we will need to use selenium. We need to make sure that the website is loaded, to do this all we will use the following code. (If you want to look at different years you can just change where is says 2023 to the year you would like to look at)

 ```
wait = WebDriverWait(driver, 10)
dropdown = wait.until(EC.element_to_be_clickable((By.ID, "stats-select-season")))
dropdown.click()

year_option = driver.find_element(By.XPATH, ".//li[text()='2023']")
year_option.click()
 ```

*If you would like more information on selenium you can find it <a href="https://selenium-python.readthedocs.io/installation.html" target="_blank">here</a>. *

Now that we have the appropriate table, we want to use the package beautiful soup to get the htlm and information from the table. Using the following code we create the beautiful soup object and get the table.

```
soup = BeautifulSoup(driver.page_source, 'html.parser')
table = soup.find('table')
```

We can use the find and find all commands from the beautiful soup package to first get the headers from the table.

```
headers = []
head = table.find('thead')
all = head.find_all('th')

for row in all:
    name = row.find('div').text
    headers.append(name)
```
Next, we need to get the row information from the table. 

```
body = table.find('tbody')
rows = []
for row in body.find_all('tr'):
    data = []
    for item in row.find_all('td'):
        thing = item.text
        data.append(thing)
    rows.append(data)
```
Finally, we will use the pandas package to create a data frame with all the information from the table in it.

```
data2023 = pd.DataFrame(rows, columns= headers)
```

Be sure to close the driver when you are finished scrapping the data. Using the following:

```
driver.close()
```

## Analysing the Data

