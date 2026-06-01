# expense_tracker.py
# Expense Tracker  A simple Python application for tracking expenses.  ## Features - Add expenses - View expenses - Calculate total spending  ## Installation  ```bash git clone https://github.com/yourusername/expense-tracker.git cd expense-tracker python expense_tracker.py
import json
import os

FILE_NAME = "expenses.json"

def load_expenses():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []

def save_expenses(expenses):
    with open(FILE_NAME, "w") as file:
        json.dump(expenses, file, indent=4)

def add_expense(expenses):
    title = input("Expense Title: ")
    amount = float(input("Amount: "))
    
    expenses.append({
        "title": title,
        "amount": amount
    })
    
    save_expenses(expenses)
    print("Expense added successfully!")

def view_expenses(expenses):
    if not expenses:
        print("No expenses found.")
        return

    print("\nExpenses:")
    for idx, expense in enumerate(expenses, start=1):
        print(f"{idx}. {expense['title']} - ₹{expense['amount']}")

def total_expenses(expenses):
    total = sum(expense["amount"] for expense in expenses)
    print(f"\nTotal Spending: ₹{total}")

def main():
    expenses = load_expenses()

    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Total Spending")
        print("4. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_expense(expenses)
        elif choice == "2":
            view_expenses(expenses)
        elif choice == "3":
            total_expenses(expenses)
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
