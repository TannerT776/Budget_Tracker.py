# Budget_Tracker.py
A Budger Tracker
import json
import os

transactions = []

def add_income(amount, description="Income"):
    transactions.append({"type": "income", "amount": amount, "description": description})

def add_expense(amount, description="Expense"):
    transactions.append({"type": "expense", "amount": amount, "description": description})

def calculate_balance():
    return sum(t["amount"] if t["type"] == "income" else -t["amount"] for t in transactions)

def view_transactions():
    for t in transactions:
        print(f"{t['type'].capitalize()}: ${t['amount']} - {t['description']}")

def save_to_file(filename="budget.json"):
    with open(filename, "w") as file:
        json.dump(transactions, file)

def load_from_file(filename="budget.json"):
    global transactions
    if os.path.exists(filename):
        with open(filename, "r") as file:
            transactions = json.load(file)
    else:
        print("File not found!")
