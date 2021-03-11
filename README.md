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

I read the csv file with the election data and converted it into a list of dictionaries. I created a for loop for each row in the csv file which added a vote to the total vote count variable, total_votes. I then printed the results.

```
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    header = next(reader)

    for row in reader:

        total_votes = total_votes + 1
        
election_results = (
    f"\nElection Results\n"
    f"-------------------------\n"
    f"Total Votes: {total_votes:,}\n"
    f"-------------------------\n"
    f"\nCounty Votes:\n")
print(election_results, end="")
```

We find the total number of votes cast to be 369,711.

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
I wrote another for loop which gets the county from the county dictionary. This loop retrieves the county vote count and calculates the percentage of votes for the county. I then printed the results.

```
for key in county_votes:

    vote_count = county_votes[key]
    
    vote_pcent = float(vote_count) / float(total_votes) * 100
        
    county_results = (
        f"{key}: {vote_pcent:.1f}% ({vote_count:,})\n")
    print(county_results)
```

We find the number and percentage of total votes for each county to be:
 - Jefferson: 10.5% (38,855)
 - Denver: 82.8% (306,055)
 - Arapahoe: 6.7% (24,801)

### County with the Largest Number of Votes
In the same for loop as above, I wrote an if statement that determined the county with the largest number of votes and then printed the results.

```
for key in county_votes:

    vote_count = county_votes[key]
    
    vote_pcent = float(vote_count) / float(total_votes) * 100
        
    county_results = (
        f"{key}: {vote_pcent:.1f}% ({vote_count:,})\n")
    print(county_results)
    
    if (vote_count > county_largest_votes):
        county_largest_votes = vote_count
        county_largest_turnout = key
        
county_turnout_summary = (
    f"\n-------------------------\n"
    f"Largest County Turnout: {county_largest_turnout}\n"
    f"-------------------------\n"
)
print(county_turnout_summary)
```
We find the county that Denver is the county with the largest number of votes.
