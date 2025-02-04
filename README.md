# Introduction

The purpose of this project is to evaluate and compare the latency of different API calls to see the influence of certain types of calls in particular the calls from CloudFlare.
  
 We will also see if the difference in latency is significant in comparison of the difference of latency due to different types of wifi connection (wifi or ethernet cable for example).
  
## Requirements

In order to compare the API calls, we need to do a wide number of requests to get a statistical point of view of the calls and get a general tendency like the mean or the variance.
  
Also, we have to get realise the API requests simultaneously because the latency is not constant over time and we want to avoid a difference due to a problem occured at a time t. It is also necessary as we want to compare each peaks of latency time eventually.

## Structure

### rapport.ipynb

This is the main file containing a jupyter notebook with all the imports and functions in order to compare all the latencies of the different APIs in config.json.

### config.json

JSON file that contains all the data the user wants to give in input in order to get all the information in rapport.ipynb working. An example of the code in this file is :

```json

{
    "execution":{
        "number" : 100,
        "timeout": 2,
        "test_reference" : "API 1",
        "name" : "wifi"
    }, 
    "APIs":{
        "API Cloud Flare":{
            "url":"https://api2",
            "color":"blue"
        },
        "API Intra":{ 
            "url" : "https://api2",
            "color":"red"
        }
    }
}

```

Where "execution" gives the main global variables and "APIs" gives the information concerning the APIs.
  
In "execution" we have :

* "number" which represents the number of calls that we will realize for each API.
* "timeout"
* "test_reference" which represents the main API reference from which we are going to compare the performances of the other APIs.
* "name" which can have the value "wifi" or "ethernet". This value shows the type of connexion that we executed (via the wifi or the ethernet cable). The type of connexion has a significative impact over the latencies.

In "APIs" we have the different APIs called. The attributes of those APIs are :

* "url" the url which allows to call the API.
* "color" which will give the color of the plots of this API.

## Results

### Histogram

This plot has the histogram of the frequency of the calls over time. It allows us to see the general tendency of the time latencies of all the API calls.
  
The more the graph is on the left the faster the API call is.

### Boxplots

This plot shows the boxplots of all the API calls. the red line indiquates the median value and the box shows the interval of the values in between the first and third quartile.
  
We also ploted a rounded walue of the median and mean of each API on the right.  

### Cumulative Distribution Function

The Cumulative Distribution Function is a concept used in statistics to describe the probability that a random variable takes the value less than or equal to a certain value.

The CDF of a random variable X is a function F(x) that gives the probability that X is less than or equal to x. Formally, for a continuous variable :

$$
F(x) = P(X \leq x)
$$

In this case, the more the curve is on the left the faster is the latency of the calls as here we plotted the CDF over time.

### Response times over time

This plot shows the time latency of each call of every API. It allows us to see the difference over time of each call.

### Heatmap

This plot shows the time latency of each call of every API in a colorfull way. It allows us to identify fast at which time the call was long and if at those times it impacted all the APIs or just a few.
