# Election Audit Results with Python

Data analysis using Python is cleaner and provides better version control than VBA in Excel. Python is faster than Excel for data pipelines, automation and calculating complex equations and algorithms. Python is open-source, consistent and accurate in the execution of code, so its easy for any users to replicate or modify the original code in future.

## Overview of Project

Tom is a **Colorado Board of Elections** Employee who is doing the **Election Audit** for Colorado Congressional District Election. So, we have a list of data with "Ballot ID, County and Candidate Name". Tom and his manager Seth is interested to find the below details out of the election result data.

  •	Total number of votes cast

  •	Candidates with their total and percentages of vote received
  
  •	Each County's total and percentage of votes 
  
  •	Largest turnout County based on total votes 
  
  •	The winner of the election based on popular vote
 
### Purpose

Tom wants to perform the Analysis based on County as well as Candidates and it will be easy for him to do it with Python. He need to submit the Election Audit results to Election Board, so having the results in text file and displaying in the terminal makes the work easy and clean. 

Also, he may want to refactor the script to make it generic for any election. 

## Analysis 

As there are large number of data for many candidates, counties and each have corresponding vote counts, we may need to create a list, dictionories to store and use in the program. Also, inititalizing all the variable is also important.

![PyPoll_Challenge_Arrays](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_Arrays.png)

* When we are reading through the row of datas, we need to get the unique Candidate names and count their corresponding votes. Once we find the next unique candidate, we need to initialize the Votes count and start counting for the new candidate. Below is the piece of code, with condition statement to perform this logic.


       if candidate_name not in candidate_options:
            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0
            
       Add a vote to that candidate's count
       candidate_votes[candidate_name] += 1


* As like the Candidates, we need to get the County list and the Votes registered in each County.

![PyPoll_Challenge_County](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_County.png)

* Once the Votes are counted for each candidate and county, we need to write the result in terminal as well as in a separate text file for Election Commission.

      for candidate_name in candidate_votes:
          # Retrieve vote count and percentage
          votes = candidate_votes.get(candidate_name)
          vote_percentage = float(votes) / float(total_votes) * 100
          candidate_results = (
              f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

          # Print each candidate's voter count and percentage to the terminal.
          print(candidate_results)
          #  Save the candidate results to our text file.
          txt_file.write(candidate_results)

* For County calculations, we need to perform the same checking and write the result in the output file. Below is the code for County: 

![PyPoll_Challenge_Write_County](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_write_County.png)

* Finally we need to write the Winning candidate details in the terminals and the output text file:

  **Determine winning vote count, winning percentage, and candidate.**

          if (votes > winning_count) and (vote_percentage > winning_percentage):
              winning_count = votes
              winning_candidate = candidate_name
              winning_percentage = vote_percentage

  **Print the winning candidate (to terminal).**

          winning_candidate_summary = (
              f"-------------------------\n"
              f"Winner: {winning_candidate}\n"
              f"Winning Vote Count: {winning_count:,}\n"
              f"Winning Percentage: {winning_percentage:.1f}%\n"
              f"-------------------------\n")
          print(winning_candidate_summary)
          # Save the winning candidate's name to the text file
          txt_file.write(winning_candidate_summary)

Performing the calculations and writing the report in the above methods will give us the **Election Audit** results in the terminal as well as in the **Election_results** text file for Election Commission.

## Challenges

* Finding the correct way to automate the whole process and getting the result with a minimum run time is little challenging. But this helps us to try doing the things in many ways, which results in better solution. 

* We have to make sure the data is sorted in proper order to find the unique Candidates, Counties and Votes. 
