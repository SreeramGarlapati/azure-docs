---
title: Analytics - the powerful search tool of Azure Application Insights | Microsoft Docs
description: 'Overview of Analytics, the powerful diagnostic search tool of Application Insights. '
services: application-insights
documentationcenter: ''
author: CFreemanwa
manager: carmonm

ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: sewhee

---
# Analytics in Application Insights
[Analytics](app-insights-analytics.md) is the powerful search feature of 
[Application Insights](app-insights-overview.md). These pages describe the
 Log Analytics query language. 

* **[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.
* **[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.
* **[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.


## Queries in Analytics
A typical query is a *source* table followed by a series of *operators* separated by `|`. 

For example, let's find out what time of day the citizens of Hyderabad try our web app. And while we're there, let's see what result codes are returned to their HTTP requests. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days. 

> [!NOTE]
> To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.
>

Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:

![Choose bar chart, x and y axes, then segmentation](./media/app-insights-analytics/020.png)

Looks like our app is most popular at lunchtime and bed-time in Hyderabad. (And we should investigate those 500 codes.)

There are also powerful statistical operations:

![Results of statistical query](./media/app-insights-analytics/025.png)

The language has many attractive features:


* [Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.
* [Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.
* Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).
* Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.
* Immediate and powerful visualizations.
* [Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).
* [Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).
* There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.


## Connect to your Application Insights data
Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights: 

![Open portal.azure.com, open your Application Insights resource, and click Analytics.](./media/app-insights-analytics/001.png)


## Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## Query examples

Try these walkthroughs to illustrate the power of using Analytics:

 *	[Automatic diagnostics of spikes and step jumps in requests durations](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *	[Analyzing performance degradations with time series analysis](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *	[Analyzing application failures with autocluster and diffpatterns](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *	[Advanced shape detections with time series analysis](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *	[Using sliding window operations to analyze application usage (rolling MAU/DAU etc)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *	[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *	[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *	[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *	[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## Next steps
* We recommend you start with the [language tour](app-insights-analytics-tour.md). 
* More about [using Analytics](app-insights-analytics-using.md). 
* [Language reference](app-insights-analytics-reference.md). 
