---
layout: post
title:  "Currency Converter Program in Python"
subtitle: "Self updating Currency Converter Program in Python for CLI"
date:   2014-11-28 20:20:40
tags:
  - Python
  - Code
  - Python programming
categories: Python
tags: [python, programming, code]
 
---
Recently I find myself traveling quite a bit internationally. I needed a program to quickly convert my money into the currency of the country I happen to visit at the moment. I took advantage of this need to practice my coding skills in Python. In this post I explain how I did  it.

I'm always refining the code. You can find the most updated version on this program on [Github](https://github.com/FedericoPaini/Python/blob/master/currencyExchangeCalculator.py).

###Business requirements/user stories

1. As I user I need to be able to put in any amount I desire and see the resulted converted output on screen
* As a user I need a program for CLI in which converts any amount to a destination currency of my choice (i.e.: US Dollars to Euros)
  * Needs to convert a source currency to a destination currency 
  * Needs to have a menu to pick what conversion rate to use 
  * The output needs to be formatted (i.e: $3,235.50)
* The conversion rate used should not be more the 24 hours old


###How the program works

The user gets prompted to chose from a menu of possible conversions as shown in Fig. 1 

![Fig.1](http://codecoms.com/wp-content/uploads/2014/09/screen1-300x155.png "Fig.1 Main Menu")


After the user has chosen which currency to convert the prompt asks for the amount to convert as shown in Fig.2


![Fig.2](http://codecoms.com/wp-content/uploads/2014/09/screen2-300x183.png "Fig.2 The user choses the amount to convert to the desired currency")

When the user hits return the calculated amount converted in the desired currency is shown along with the conversion rate as shown in Fig.3

![Fig.3](http://codecoms.com/wp-content/uploads/2014/09/screen3-300x47.png "Fig.3 Final screen with the converted amount.")

###Code Explanation

* __conv_rates.txt__. is the text database in which I store all the currency conversion rate, line by line comma delimited:

 ```
 USD-EUR,0.788420
 EUR-USD,1.268360
 USD-GBP,0.615612
 GBP-USD,1.624400
 USD-INR,61.384240
 INR-USD,0.016291
 ```
 * **create_exchange_dict()**. In this function read the *conv_rates.txt* and create the Exchange Rate Dictionary:
 
 ```
 def create_exchange_dict():
	exchange_rates_dict = {}
	conversion_rates = open (file, 'r') #open file read only
	
	for line in conversion_rates:
		exchange_rates_dict[line.split(",")[0]] = line.split(",")[1]

	conversion_rates.close()
	return exchange_rates_dict
```

* **grab_web_rates()**. This is the heart of the program. The function goes online, grabs the exchange rates from a live website and saved them into *conv_rates.txt*. To do this I use the Python libraries  `urllib2` and `re`. In this instance I only grab the first 23 lines to avoid copying the  whole website.

```python
def grab_web_rates():
	conversion_rates = open (file, 'w')
	web = urllib2.urlopen('http://www.x-rates.com/table/?from=USD')
	html = web.read()
	line = 1
	titles = re.findall(r'<td class=\'rtRates\'><a href=\'/graph/\?from=(.*?)</td>', html)
	for title in titles:
		title = title.replace("amp;to=", "")
		title = title.replace("&", "-")
		title = title.replace("'>", ",")
		title = title.replace("</a>", " ")
		title = title.replace("  ", "")
		title = title.rstrip()
		conversion_rates.write(title + ' \n')
		line += 1
		if line >= 23:
			break
	conversion_rates.close()
```

* **get_result(choice, amount)**. Based on the amount and the exchange rate chosen by the user this function returns the desired amount in the new currency based on the exchange rate in the database. Returns an error if the rate is not found.

```python
def get_result(choice, amount):
	dict = create_exchange_dict()
	for exchange,rate in dict.items():
		if exchange == choice:
			result = amount * float(rate)
			return rate, result
			break
		else:
			error = "Exchange not found! -get_result()- "
```