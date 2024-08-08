# Data Analytics Job Survey Analysis 
[![Read on Medium](https://img.shields.io/badge/Read%20on-Medium-1DA1F2?logo=medium)](https://medium.com/@mahhinshahzad/data-analytics-job-survey-analysis-with-power-bi-dc7fbd7cf1a4)


I always had a deep curiosity and interest in analyzing data related to actual Data Analyst roles, but I could never find it. There were always resources like Stack Overflow survey data and other general ones, but even the most escalated survey would be related to Data Science. So, I planned to extract proportions from multiple data sources and then start the analysis. Thankfully, I recently found out about this survey done by [Alex The Analyst](https://github.com/AlexTheAnalyst)
 , where he collected this relatively new data, and I had to take a look into it.

The biggest problem with this data is that it is quite small and limited, with 630 respondents, out of which **400** are exactly Data Analysts. My experience with Power BI is relatively less than other tools, but I still created this in BI because why not (actually because it is just so popular).

## Data Cleaning
The most involved yet satisfying thing about the job is the cleaning. After working with **Power Query**, I realized how much I just love cleaning in *pandas* and Excel, the memory, and speed issues with them. Oh, come on, they are just pure love, you crazy.

So yeah, you can use these fancy UI tools of Power Query for removing duplicates directly, removing nulls, and changing types, but wait till you get to normalization. That was the biggest problem with this data or even survey data in general—the custom information actually making sense of it is something. Well, that is why people run to sales data so much. Ahh, those decimals and time series.

We had two options: either replace every single value in Power Query, or we could have done something smart.

Here is a snippet of the M code used for normalization:

```m
= Table.ReplaceValue(#"Reordered Columns1", \\ Name of your perv step 
    each [#"Updated Jobs"],
    each if Text.Contains([#"Updated Jobs"], "Other (Please Specify):Retail") then "Retail"
         else if Text.Contains([#"Updated Jobs"], "Other (Please Specify):Automotive") then "Automotive"
         else if Text.Contains([#"Updated Jobs"], "Other (Please Specify):Consulting") then "Consulting"
         else [#"Updated Jobs"],
    Replacer.ReplaceText,
    {"Updated Jobs"})
```
We used this code in our query panel and fixed all values in a blink. Similarly, we fixed normalization for other things, and for things that were way too difficult to fix, we just delimited by our custom delimiter, so all their customer unwanted instructions are now called "others."

Next, we fixed salary by using an average of salary from both ranges. And of course, we handled the null values, duplicates, and data types.

# The Fun Part: Visualizations
Now seriously, did I call data cleaning fun? Come on, that is why it is said that skimming through text is never a good idea. I want your full focus on this now!!

What was the fun part? Yeah, the visuals. Oh, there is nothing fun in them. If your data is cleaned, just close your eyes, randomly select some visuals and drag some data fields onto them from left to right. There you are with your well-crafted visuals.

Similarly, I got mine, which are tada tada. All of them are created here.

![screenshot  Report](https://github.com/Mahhin1010/Data-Analytics-Job-Survey-Analysis/blob/main/Reportmain.jpg)

Some DAX queries you might also need to write if you want to show multiple rating questions in a single visual:
```
Count_Very_Unsatisfied = 
CALCULATE(
    COUNTROWS('Data Pivot Quest'),
    'Data Pivot Quest'[Score] >= 1 && 'Data Pivot Quest'[Score] <= 2
)
\\ Yeah, my rating scale was till 10. And that was it for the visuals.

```

<br><br><br>

## Insights
Here are some insights that will blow your mind, like for real:

- The majority of people use Python and R in data-related jobs. Bet you thought it was Java.
- Tech, finance, and healthcare are the biggest fields for data-related jobs. Who would have thought?
- Data Scientists and Data Engineers are typically making more money than Data Analysts. You expected that, but you did not expect that even Data Architects would make more.
- The average age of the respondents was 29.87 years old, not 30, but 29.87.

### Additional Insights:

- The majority of data-related people are not satisfied with their jobs; only **27%** are.
- Respondents seem to be quite happy with their **coworkers** and *learning new things*.

<br><br><br>

## Conclusion

The best feature among this is being able to filter down. With the tree map, I can trim down on the specific niche country, see the stats for the specific part rather than the whole general information. But since Power BI has made it so easy for everyone to host their dashboards, we won't be able to use that. You'll need to download the PBIX file from here and run it directly on your Power BI desktop.







