# Similarweb
Python wrapper for the [SimilarWeb API](https://developer.similarweb.com/doc).

## Usage

Create a client object for the API you'd like to use:

#### Ready to go
* Traffic: `traffic_client = TrafficClient("your_api_key")`
* Content: `content_client = ContentClient("your_api_key")`

#### In development
* Mobile: `mobile_client = MobileClient("your_api_key")`
* Sources: `sources_client = SourcesClient("your_api_key")`

## Traffic Client in Action

Let's set up the traffic client object and some variables we'll be using throughout:

```python
>>> from similarweb import TrafficClient
>>> traffic_client = TraffiClient("my_api_key")
>>> url = "example.com"     # <~ no "www." or "http://"
>>> gr = "monthly"          # <~ or "weekly" or "daily"
>>> start_month = "11-2014" # <~ M-YYYY
>>> end_month = "12-2014"   # <~ M-YYYY
>>> md = False              # or True if you want main domain ONLY
```

Get the number of estimated visits for the requested domain with `.visits`:

```python
>>> traffic_client.visits(url, gr, start_month, end_month, md)
{"2014-11-01": 123456789, "2014-12-01": 123456788}
```

Get the global rank, country rank, traffic geography, traffic reach and traffic sources distribution with `.traffic`:

```python
>>> traffic_client.traffic(url)
{
 "GlobalRank": 2,
 "CountryCode": 840,
 "CountryRank": 1,
 "TopCountryShares": {
  "840": 0.4321,
  "356": 0.3210,
  # ... many more country code-share pairs
  "876": 6.8674e-7,
  "10": 0
 },
 "TrafficReach": {
  "01/08/2014": 0.1234,
  "08/08/2014": 0.1233,
  # ... many more date-reach pairs
  "23/01/2015": 0.1232,
  "30/01/2015": 0.1231
 },
 "TrafficShares": {
  "Search": 0.1043,
  "Social": 0.0302,
  "Mail": 0.0041,
  "Paid Referrals": 0.0016,
  "Direct": 0.6771,
  "Referrals": 0.1826
 },
 "Date": "01/2015"
}
```

Get the average pageviews for the requested domains with `.page_views`:

```python
>>> traffic_client.page_views(url, gr, start_month, end_month, md)
{"2014-11-01": 14.1234, "2014-12-01": 14.1233}
```

Get the average visit duration at the requested domain with `.visit_duration`:

```python
>>> traffic_client.visit_duration(url, gr, start_month, end_month, md)
{"2014-11-01": 987.654321, "2014-12-01": 987.654320}
```

Get the average bounce rate for the requested domain with `.bounce_rate`:

```python
>>> traffic_client.bounce_rate(url, gr, start_month, end_month, md)
{"2014-11-01": 0.1234, "2014-12-01": 0.1233}
```

## Content Client in Action

Let's set up the content client object and some variables we'll be using throughout:

```python
>>> from similarweb import ContentClient
>>> content_client = ContentClient("my_api_key")
>>> url = "example.com"     # <~ no "www" or "http://"
```

Get sites similar to the requested domain along with similarity scores:

```python
>>> content_client.similar_sites(url)
{"example2.com": 0.9988776655,
 "example3.com": 0.987654321,
 # many other similar sites and their similarity scores...
 "exampleN.com": 0.2109876543}
```

Get sites and their affinity score frequently visited by users of the requested domain:

```python
>>> content_client.also_visited(url)
{"example2.com": 0.00123456,
 "example3.com": 0.00012345,
 # many other frequently-visited sites and their frequency scores...
 "exampleN.com": 0.00001234}
```

Get tags and their score for the requested domain:

```python
>>> content_client.tags(url)
{"shrimp": 0.987654321,
 "white wine": 0.987654320,
 # many other tags and their scores...
 "dilly": 0.098765432}
```

Get the category for the requested domain:

```python
>>> content_client.category(url)
{"Category": "Shrimp/White Wine"}
```

Get the category and rank for the requested domain:

```python
>>> content_client.category_rank(url)
{"Category": "Shrimp/White Wine",
 "CategoryRank": 1}
```
