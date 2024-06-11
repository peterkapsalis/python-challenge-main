import csv

csv_path = r"C:\Users\User\Desktop\python-challenge-main\python-challenge-main\PyPoll\election_data.csv"

total_votes = 0
candidates = {}
winner = None

with open(csv_path, newline='') as csvfile:
    csvreader = csv.reader(csvfile)
    header = next(csvreader)

    for row in csvreader:
        total_votes += 1
        candidate = row[2]
        if candidate in candidates:
            candidates[candidate] += 1
        else:
            candidates[candidate] = 1

max_votes = 0
for candidate, votes in candidates.items():
    if votes > max_votes:
        max_votes = votes
        winner = candidate

print(f"Total Votes: {total_votes}")
for candidate, votes in candidates.items():
    percentage = (votes / total_votes) * 100
    print(f"{candidate}: {percentage:.2f}% ({votes})")
print(f"Winner: {winner}")
