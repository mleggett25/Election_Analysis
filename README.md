# Election Analysis with Python

## Overview of Election Audit

### Purpose
The purpose of this election analysis audit was to complete the following tasks for a recent local congressional election:

 1. Calculate the total number of votes cast.
 2. Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.
 3. Determine which county had the largest number of votes.
 4. Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.
 5. Determine which candidate won the election and calculate their vote count and precentage of the total votes.

## Election Audit Results

### Total Number of Votes Cast
To calculate the total number of votes cast, I first initialized a total vote counter.

```
total_votes = 0
```

I then read the csv file with the election data and converted it into a list of dictionaries. I created a for loop for each row in the csv file which added a vote to the total vote count variable, total_votes.

```
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    header = next(reader)

    for row in reader:

        total_votes = total_votes + 1
```

Using this code, we find the total number of votes cast to be 369,711.

### Number of Votes and Percentage of Total Votes for Each County
To provide a breakdown of the number of votes and the percentage of total votes for each county, I first created a list for the counties and a dictionary for the county votes.
```
county_list = []
county_votes = {}
```

In the same script that was used to calcuate the total votes, I initialized a variable to get the county name from each row.

```
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    header = next(reader)

    for row in reader:

        total_votes = total_votes + 1
        
        county_name = row[1]
```

I then wrote an if statement within the existing for loop that checks if the county matches any existing county in the county list. If the county is not in the county list, it is added to the list of counties and begins tracking and adding to the counties vote count.

```
    if county_name not in county_list:
        
        county_list.append(county_name)
        
        county_votes[county_name] = 0
        
    county_votes[county_name] += 1
    
```
Using this code, we find the number and percentage of total votes for each county to be:
 - Jefferson: 10.5% (38,855)
 - Denver: 82.8% (306,055)
 - Arapahoe: 6.7% (24,801)


