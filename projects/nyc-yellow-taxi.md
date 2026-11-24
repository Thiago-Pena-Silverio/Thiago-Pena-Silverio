# New York City yellow taxi trips, 2022–2023

A teammate and I used Microsoft Fabric, PySpark and Power BI to compare New York City yellow taxi trips across two years. We wanted to know whether the number of journeys, their duration and the amounts passengers were charged changed together.

## What we found

| Measure | 2022 | 2023 |
| --- | ---: | ---: |
| Recorded trips after cleaning | 39,623,537 | 38,294,557 |
| Average recorded charge per trip | $21.66 | $28.46 |
| Average duration | 17.33 min | 17.46 min |

Trip volume fell by 3.4%. The average recorded charge rose by $6.80, while average journey time changed by less than ten seconds. The comparison describes the trips in the records. Several factors could affect charges, and the analysis did not isolate their effects.

## From monthly files to a report

1. We combined 24 monthly Parquet files in a Fabric Lakehouse. The yearly files used different numeric types for some identifiers and different capitalisation for the airport fee field. We aligned the schemas and kept the source filename for each record.
2. We checked timestamps and exact duplicates before counting trips. Of 77,966,324 input records, 77,918,094 remained after removing three extra duplicate rows, 623 pickups outside the study period and 47,604 records whose drop-off time was at or before pickup.
3. We modelled one row per trip, with a date dimension and separate pickup and drop-off zone dimensions. The Power BI report let readers compare months, boroughs and charges. We grouped trips by pickup date because a file can contain trips from a different month.

## A data quality decision

The report flagged an unusual spike in recorded card tips in December 2022. We kept the source values and called out the anomaly in the report. A comparison of driver earnings would need other information, including cash tips.

The public source includes the monthly files, taxi-zone lookup and field definitions. [NYC Taxi and Limousine Commission trip records](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
