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

In the same script that was used to calculate the total votes, I initialized a variable to get the county name from each row.

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

We find that Denver is the county with the largest number of votes.

### Number of Votes and Percentage of Total Votes for Each Candidate
To provide a breakdown of the number of votes and percentage of total votes for each candidate, I first created a list for the candidate options and a dictionary for the candidate votes.

```
candidate_options = []
candidate_votes = {}
```

Within the for loop I created to loop through each row in the csv file, the loop extracted the candidate name from each row. I created an if statement that checks if the candidate name matches any existing candidate name in the candidate options list. If the candidate is not in the candidate options list, it is added to the list and begins tracking and adding to the candidates vote count.

```
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    header = next(reader)

    for row in reader:

        candidate_name = row[2]

        if candidate_name not in candidate_options:

            candidate_options.append(candidate_name)

            candidate_votes[candidate_name] = 0

        candidate_votes[candidate_name] += 1
```

I then wrote another for loop which gets the candidate name from the candidate dictionary. This loop retrieves the candidate vote count and calculates the percentage of votes for the candidate. I then printed the results.

```
for candidate_name in candidate_votes:

    votes = candidate_votes.get(candidate_name)
    vote_percentage = float(votes) / float(total_votes) * 100
    candidate_results = (
        f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

    print(candidate_results)
```
We find the number and total percentage for each candidate to be:
- Charles Casper Stockham: 23.0% (85,213)
- Diana DeGette: 73.8% (272,892)
- Raymon Anthony Doane: 3.1% (11,606)

### Winning Candidate

In the same for loop as above, I wrote an if statement that determined the county with the largest number of votes and then printed the results.

```
for candidate_name in candidate_votes:

    votes = candidate_votes.get(candidate_name)
    vote_percentage = float(votes) / float(total_votes) * 100
    candidate_results = (
        f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

    if (votes > winning_count) and (vote_percentage > winning_percentage):
        winning_count = votes
        winning_candidate = candidate_name
        winning_percentage = vote_percentage

winning_candidate_summary = (
    f"-------------------------\n"
    f"Winner: {winning_candidate}\n"
    f"Winning Vote Count: {winning_count:,}\n"
    f"Winning Percentage: {winning_percentage:.1f}%\n"
    f"-------------------------\n")
print(winning_candidate_summary)
```

We find that the winner of the election was Diana DeGette with 272,892 votes (73.8% of the total vote).

## Election Audit Summary
I propose that this script be used to analyze future election data. Because most of the code in the script is not hard coded, the script can be run with any election data with little modification. We can modify the script in a couple ways to help it be more useful in other elections. One way to modify the script is to use the glob function which will allow us to open and concatenate multiple data files. This could be useful because each counties election data would come reported in its own data file. Instead of manually combining all of the counties data into one file and allowing for potential human error, we can use the glob function. The code would look something like this:

```
import glob
import os
import pandas as pd

# Path to the file directory
mycsvdir = 'csvdir'

# Get all the csv files in that directory (assuming they have the extension .csv)
csvfiles = glob.glob(os.path.join(mycsvdir, 'election*.csv'))

# Loop through the files and read them in with pandas
dataframes = []  # a list to hold all the individual pandas DataFrames
for csvfile in csvfiles:
    df = pd.read_csv(csvfile)
    dataframes.append(df)

# Concatenate them all together
result = pd.concat(dataframes, ignore_index=True)

# Print out to a new csv file
result.to_csv('election_results_all.csv')
```
Source: https://stackoverflow.com/a/53190147/15171602

We would then set the existing file_to_load variable equal to the new election_results_all.csv file.

Another way to modify the script is to use the input function to ask the user if they want to write the election results to the election_analysis.txt file. This could be useful in preventing unwanted overwriting of the txt file while working with and running the code. The code would look like this:

```
write_results = input("Would you like to write the results to the election_analysis.txt file?")
if write_results == "Yes":
    txt_file.write(election_results)
    for key in county_votes:
        txt_file.write(county_results)
    txt_file.write(county_turnout_summary)
    for candidate_name in candidate_votes
        txt_file.write(candidate_results)
    txt_file.write(winning_candidate_summary)
elif write_results == "No":
    Pass
```


