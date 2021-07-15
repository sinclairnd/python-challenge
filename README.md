# python-challenge
# Format:
# Column 1: Jan-2010
# Column 2: 867884
    
# Total number of months in the data set
# Net total amount of P&L over the entire period
# Calculated change of P&L over the entire period
# Average of calculated change of P&L over the entire period
# Greatest increase in profits (date + amount) over the entire period
# Greatest decrease in losses (date + amount) over the entire period

### Example of finished output
#   Financial Analysis
#   ----------------------------
#   Total Months: 86
#   Total: $38382578
#   Average  Change: $-2315.12
#   Greatest Increase in Profits: Feb-2012 ($1926159)
#   Greatest Decrease in Profits: Sep-2013 ($-2196167)

import os
import csv

with open ('budget_data.csv') as csvfile:
    reader = csv.reader(csvfile, delimiter=",")
    rows = list(reader)
    total_months = 0
    total_profits = 0
    greatest_increase_month = ""
    greatest_increase_profit = 0
    greatest_decrease_month = ""
    greatest_decrease_lose = 0
    
    previous_profit = None
    profit_change = []
    profit_change_month = []
    
    for row in rows[1:]:
        total_months += 1
        total_profits += int(row[1])
        
        if previous_profit != None:
            profit_change.append(int(row[1]) - previous_profit)
            profit_change_month.append(row[0])
        previous_profit = int(row[1])
        
    average_change = sum(profit_change) / len(profit_change)
        
    greatest_increase_profit = max(profit_change)
    greatest_decrease_lose = min(profit_change)
    
    greatest_increase_month = profit_change_month[profit_change.index(greatest_increase_profit)]
    greatest_decrease_month = profit_change_month[profit_change.index(greatest_decrease_lose)]
    
    print("Financial Analysis")
    print("----------------")
    print("Total months: " + str(total_months))
    print("Total profits: " + str(total_profits))
    print("Average Change: " + str(round(average_change, 2)))
    print("Greatest Increase in Profits: " + str(greatest_increase_month) + " ($" + str(greatest_increase_profit) + ")")
    print("Greatest Decrease in Profits: " + str(greatest_decrease_month) + " ($" + str(greatest_decrease_lose) + ")")
    
    #--------------------
    
import os
import csv

with open ('election_data.csv') as csvfile:
    reader = csv.reader(csvfile, delimiter=",")
    rows = list(reader)
    total_votes = 0
    candidates_with_votes = set()
    won_percentage = {}
    count_per_candidate = {}
    highest_vote_candidate = ""
    highest_vote_votes = 0
    
    for row in rows[1:]:
        total_votes += 1
        candidates_with_votes.add(row[2])
        if row[2] not in count_per_candidate:
            count_per_candidate[row[2]] = 0
        count_per_candidate[row[2]] += 1
    
    for candidate in candidates_with_votes:
        if count_per_candidate[candidate] > highest_vote_votes:
            highest_vote_votes = count_per_candidate[candidate]
            highest_vote_candidate = candidate
        won_percentage[candidate] = 100 * count_per_candidate[candidate] / total_votes

    print("Election Results")
    print("----------------")
    print("Total Votes: " + str(total_votes))
    print("----------------")
    
    for candidate in candidates_with_votes:
        print(candidate + " " + str(round(won_percentage[candidate], 2)) + "% (" + str(count_per_candidate[candidate]) + ")")
    
    print("----------------")
    print("Winner: " + highest_vote_candidate)
        
