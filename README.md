# Election_Analysis

The code that was used for this analysis is [PyPoll Challenge - Election Analysis](https://github.com/ninicholasas/Election_Analysis/blob/main/PyPoll_Challenge.py)


## __Overview__
### Goal
The goal for this challenge is to report the total numberof votes cast, the total nember of votes for each andidate, the percentage of votes for each andidate, and the winner of the election based on the popular vote from the U.S. congressional precint in Colarado using Python.
### Data
The given csv file([election results csv](https://github.com/ninicholasas/Election_Analysis/blob/main/Resources/election_results.csv)) was consisted of 3 columns; <br />
  * Ballot ID
  * County
  * Candidate
## __Election-Audit Results__
Below is the result for this analysis.
<img width="1029" alt="PyPoll_Challenge_scsh" src="https://user-images.githubusercontent.com/110373282/204063762-66e8f56b-f462-4bdf-9f7c-e9083547debc.png">

* __How many votes were cast in this congressional election?__<br />
    369,711 votes. The total votes were calculated by creating a counter for the total votes and use a for-loop to iterate through the give csv file.
  
  ```
    # Initialize a total vote counter.
    total_votes = 0
    # Read the csv and convert it into a list of dictionaries
    with open(file_to_load) as election_data:
      reader = csv.reader(election_data)

      # For each row in the CSV file.
      for row in reader:
        # Add to the total vote count
        total_votes = total_votes + 1
  ```
* __Provide a breakdown of the number of votes and the percentage of total votes for each county in the precint.__<br />
    County Votes; Jefferson: 10.5% (38,855), Denver: 82.8% (306,055), Arapahoe: 6.7% (24,801)<br />
  The number of votes for each county was returned by if statement while the for-loop to create a list of the counties and creating a dictionary for each county to hold the votes.
  ```
    # Read the csv and convert it into a list of dictionaries
    with open(file_to_load) as election_data:
        reader = csv.reader(election_data)

        # Read the header
        header = next(reader)

        # For each row in the CSV file.
        for row in reader:

            # Add to the total vote count
            total_votes = total_votes + 1

            # Get the candidate name from each row.
            candidate_name = row[2]

            # 3: Extract the county name from each row.
            county_name = row[1]

            # If the candidate does not match any existing candidate add it to
            # the candidate list
            if candidate_name not in candidate_options:

                # Add the candidate name to the candidate list.
                candidate_options.append(candidate_name)

                # And begin tracking that candidate's voter count.
                candidate_votes[candidate_name] = 0

            # Add a vote to that candidate's count
            candidate_votes[candidate_name] += 1

            # 4a: Write an if statement that checks that the
            # county does not match any existing county in the county list.
            if county_name not in counties:

                # 4b: Add the existing county to the list of counties.
                counties.append(county_name)

                # 4c: Begin tracking the county's vote count.
                county_voter_count[county_name] = 0

            # 5: Add a vote to that county's vote count.
            county_voter_count[county_name] += 1
  ```
    After we have got each vote counts for each county, we divide it with the total votes to get the percentage.
  ```
    for county_name in counties:
        # 6b: Retrieve the county vote count.
        votes = county_voter_count[county_name]
        # 6c: Calculate the percentage of votes for the county.
        vote_percentage = float(votes) / float(total_votes) * 100

         # 6d: Print the county results to the terminal.
        county_results = f"{county_name}: {vote_percentage:.1f}% ({votes:,})\n"
  ```
* __Which county had the largest number of votes?__<br />
    From the results we can tell that Denver had the largest number of votes. But in the code I used a if statement to overright the variables if the votes and vote percentage was higher than the previous.
    ```
      # 6f: Write an if statement to determine the winning county and get its vote count.
      if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_percentage = vote_percentage
            largest_county = county_name
    ```
* __Provide a breakdown of the number of votes and the percentage of the total votes each candidate recieved.__
  Candidate Votes; Charles Casper Stockham: 23.0% (24,801), Diana DeGette: 73.8% (24,801), Raymon Anthony Doane: 3.1% (24,801)<br />
  The method that was used to get the above result was the same as the method that was used to get the County Votes. The difference is that the county was based from the 2nd row in the csv file and the candidate is based on the 3rd row.
    ```
      # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]
    ```
* __Which candidate won the election, what was their vote count, and what was their percentage of the total votes?__<br />
  Winner: Diana DeGette<br />
  Winning Vote Count: 272,892<br />
  Winning Percentage: 73.8%<br />
This result was returned from the same code with the country with the largest number of votes.
One modification I needed to add was that I needed to reset the winning_count and winning_percentage to 0 on line 128 amd 129, since it was comparing the results with the counties.
  ```
    winning_count = 0
    winning_percentage = 0
  ```
## __Election-Audit Summary__

If there were an another column in the given csv file that has the State data, I could modify this code to iterate through each state, county, and candidate to make this code universal to elections over the U.S. Also, if there were a column for the candidates party, we could create a percentage of votes that went to each party. 
We could wrap this whole code with the above 2 modification and create a dictionary in the code to view all sorts of analysis, i.e. party percentage by states, vote count based on states, how many parties are in each state, etc.
