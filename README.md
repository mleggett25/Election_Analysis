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
``
total_votes = 0
``
I then read the csv file with the election data and converted it into a list of dictionaries. I created a for loop for each row in the csv file and created a variable total_votes that added to the total vote count.
``
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    header = next(reader)

    for row in reader:

        total_votes = total_votes + 1
``
Using this code, we find the total number of votes cast to be 369,711.

### Number of Votes and Percentage of Total Votes for Each County
