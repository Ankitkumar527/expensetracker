# expensetracker
import csv
import os

class ExpenseTracker:
    def __init__(self, filename='expenses.csv'):
        self.filename = filename
        self.expenses = []
        if os.path.exists(self.filename):
            self.load_expenses()

    def add_expense(self, date, category, amount, description):
        self.expenses.append({
            'date': date,
            'category': category,
            'amount': amount,
            'description': description
        })

    def view_expenses(self):
        for expense in self.expenses:
            print(f"Date: {expense['date']}, Category: {expense['category']}, Amount: ${expense['amount']}, Description: {expense['description']}")

    def save_expenses(self):
        with open(self.filename, 'w', newline='') as file:
            writer = csv.DictWriter(file, fieldnames=['date', 'category', 'amount', 'description'])
            writer.writeheader()
            writer.writerows(self.expenses)

    def load_expenses(self):
        with open(self.filename, 'r') as file:
            reader = csv.DictReader(file)
            self.expenses = [row for row in reader]

def main():
    tracker = ExpenseTracker()

    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Save and Exit")
        choice = input("Choose an option: ")

        if choice == '1':
            date = input("Enter date (YYYY-MM-DD): ")
            category = input("Enter category: ")
            amount = input("Enter amount: ")
            description = input("Enter description: ")
            tracker.add_expense(date, category, amount, description)
        elif choice == '2':
            tracker.view_expenses()
        elif choice == '3':
            tracker.save_expenses()
            print("Expenses saved. Exiting...")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
