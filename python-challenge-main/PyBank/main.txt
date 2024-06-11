import csv

csv_path = r"C:\Users\User\Desktop\python-challenge-main\python-challenge-main\PyBank\budget_data.csv"

total_months = 0
total_profit_loss = 0
previous_profit_loss = None
changes = []
dates = []
greatest_increase = {"date": None, "amount": float('-inf')}
greatest_decrease = {"date": None, "amount": float('inf')}


with open(csv_path, newline='') as csvfile:
    csvreader = csv.reader(csvfile)
    header = next(csvreader)

    for row in csvreader:
        date = row[0]
        profit_loss = int(row[1])
        dates.append(date)

        total_months += 1
        total_profit_loss += profit_loss

        if previous_profit_loss is not None:
            change = profit_loss - previous_profit_loss
            changes.append(change)

            if change > greatest_increase["amount"]:
                greatest_increase["date"] = date
                greatest_increase["amount"] = change

            if change < greatest_decrease["amount"]:
                greatest_decrease["date"] = date
                greatest_decrease["amount"] = change

        previous_profit_loss = profit_loss

average_change = sum(changes) / len(changes) if changes else 0

print(f"Total Months: {total_months}")
print(f"Total Profit/Loss: ${total_profit_loss}")
print(f"Average Change: ${average_change:.2f}")
print(f"Greatest Increase in Profits: {greatest_increase['date']} (${greatest_increase['amount']})")
print(f"Greatest Decrease in Profits: {greatest_decrease['date']} (${greatest_decrease['amount']})")
