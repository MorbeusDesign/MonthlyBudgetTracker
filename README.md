# Monthly Budget Tracker
The Monthly Budget Tracker is a beginner-friendly web application that helps users manage their personal finances by tracking income, expenses, and overall balance on a monthly basis. This project is ideal for new JavaScript developers who want to learn and apply fundamental programming concepts such as DOM manipulation, event handling, data validation, and real-time calculations in a practical, hands-on way.

<div align="center">
<img  src="https://github.com/MorbeusDesign/MonthlyBudgetTracker/blob/main/screenshot1.JPG" width="600"  alt = 'Desktop Screenshot' />
<img src="https://github.com/MorbeusDesign/MonthlyBudgetTracker/blob/main/screenshot2.JPG" width="600"  alt = 'Desktop Screenshot' />
</div>

## Features
Dynamic Expense Tracking: Add, view, and manage expenses with specific descriptions and values. The app dynamically updates the list of expenses on the user interface.
Real-Time Balance Calculation: Automatically calculates the final monthly balance as expenses and income values are entered or updated, providing immediate feedback on the user's financial status.
Input Validation: Ensures that income and expense values are positive, while the initial account balance can be negative, making it versatile for different financial scenarios.
Responsive Design: The application layout adjusts to different screen sizes, making it accessible and easy to use on both desktop and mobile devices.

## How It Works
1. **Enter Financial Data**: Users input their initial account balance, primary income, and secondary income.
2. **Add Expenses**: Users can add multiple expenses by entering a description and value for each one. These expenses are listed on the screen for easy tracking.
3. **Automatic Calculations**: The app calculates the final balance by summing up the income, subtracting the total expenses, and adjusting for the initial account balance.
4. **Real-Time Updates**: The displayed balance updates instantly whenever income or expenses are modified, ensuring an accurate financial snapshot at all times.

## Learning Objectives
This project is designed to help beginners learn and practice key JavaScript skills, including:

- DOM Manipulation: Learn how to dynamically update and interact with the HTML elements on the page.
- Event Handling: Understand how to respond to user actions, such as button clicks and input changes, to update the application state.
- Arrays and Objects: Manage data using arrays and objects, fundamental data structures in JavaScript.
- Input Validation: Implement basic input validation to ensure data integrity and improve user experience.
- Responsive Layout: Utilize CSS and media queries to create a responsive design that works well on various screen sizes.
Getting Started

## To run the Monthly Budget Tracker locally, follow these steps:

**Clone the repository:**
```bash
git clone https://github.com/yourusername/monthly-budget-tracker.git
````
**Navigate to the project directory:**
```bash
cd monthly-budget-tracker
````
**Open 'index.html' in your web browser.**

## Technologies Used
- **HTML:** For structuring the application layout and input forms.
- **CSS:** For styling the application and making it responsive across different devices.
- **JavaScript:** For adding interactivity, handling user input, performing calculations, and updating the DOM dynamically.

## Step-by-Step Explanation of the JavaScript Code

Below is a detailed breakdown of the JavaScript code used in the Monthly Budget Tracker program:

```javascript
let expenses = [];
```

1. **Declare and Initialize an Array:**  
   The variable `expenses` is declared as an empty array. This array will be used to store each expense as an object containing a description and a value. It serves as the main data structure for managing the list of expenses.

```javascript
function addExpense() {
    const description = document.getElementById('expenseDescription').value;
    const value = parseFloat(document.getElementById('expenseValue').value);

    if (description && !isNaN(value) && value > 0) {
        expenses.push({ description, value });
        updateExpensesList();
        document.getElementById('expenseDescription').value = '';
        document.getElementById('expenseValue').value = '';
        calculateBalance(); // Update the balance immediately after adding an expense
    } else {
        alert('Please enter a valid description and a positive value for the expense.');
    }
}
```

2. **Function to Add an Expense (`addExpense`):**  
   - **Retrieve Inputs:** This function gets the values from the input fields for the expense description and value.
   - **Validation:** It checks if the description is not empty, the value is a number, and the value is greater than zero. This ensures that only valid expenses are added.
   - **Add to Array:** If the input is valid, it creates an object with the description and value and adds it to the `expenses` array.
   - **Update the UI and Clear Inputs:** The function then calls `updateExpensesList()` to refresh the list of expenses displayed on the page and clears the input fields for the next entry.
   - **Recalculate Balance:** Finally, it calls `calculateBalance()` to update the displayed balance based on the new expense added.

```javascript
function updateExpensesList() {
    const list = document.getElementById('expensesList');
    list.innerHTML = '';
    expenses.forEach((expense) => {
        const item = document.createElement('li');
        item.textContent = `${expense.description}: €${expense.value.toFixed(2)}`;
        list.appendChild(item);
    });
}
```

3. **Function to Update the Expenses List (`updateExpensesList`):**  
   - **Clear Current List:** This function clears the current contents of the expenses list in the HTML by setting its inner HTML to an empty string.
   - **Display Each Expense:** It iterates over the `expenses` array using `forEach()`, creating a new `<li>` element for each expense. The list item displays the description and value of the expense, formatted to two decimal places.
   - **Update the DOM:** Each `<li>` element is then appended to the `<ul>` element with the ID `expensesList`, which updates the displayed list of expenses on the page.

```javascript
function calculateBalance() {
    const initialBalance = parseFloat(document.getElementById('initialAccountBalance').value);
    const primaryIncome = parseFloat(document.getElementById('primaryIncome').value);
    const secondaryIncome = parseFloat(document.getElementById('secondaryIncome').value);

    if (isNaN(initialBalance) || isNaN(primaryIncome) || isNaN(secondaryIncome)) {
        alert('Please ensure you enter valid values for the initial balance and incomes.');
        return;
    }

    // Calculate the total of expenses
    const totalExpenses = expenses.reduce((acc, curr) => acc + curr.value, 0);

    // Calculate the final balance for the month
    const finalBalance = initialBalance + primaryIncome + secondaryIncome - totalExpenses;

    // Display the final balance
    const balanceElement = document.getElementById('finalBalance');
    balanceElement.textContent = `Final Monthly Balance: €${finalBalance.toFixed(2)}`;
}
```

4. **Function to Calculate and Display the Final Monthly Balance (`calculateBalance`):**  
   - **Retrieve Input Values:** This function retrieves the values of the initial account balance, primary income, and secondary income from their respective input fields.
   - **Validation:** It checks whether any of the values are `NaN` (not a number). If so, it alerts the user to enter valid values and stops further execution.
   - **Calculate Total Expenses:** The function calculates the sum of all expense values in the `expenses` array using the `reduce()` method.
   - **Calculate Final Balance:** It calculates the final balance by adding the initial balance and both income sources, then subtracting the total expenses.
   - **Update Displayed Balance:** Finally, it updates the text of the `<h2>` element with the ID `finalBalance` to show the calculated balance, formatted to two decimal places.

```javascript
function validatePositiveInput(input) {
    if (parseFloat(input.value) < 0) {
        input.value = 0;
        alert('Please enter a positive value.');
    }
}
```

5. **Function to Validate Positive Inputs (`validatePositiveInput`):**  
   - **Ensure Positive Values:** This function checks if an input value is negative. If it is, the value is reset to `0`, and an alert is displayed to prompt the user to enter a positive value.
   - **Usage:** This function is called in the `oninput` event of income and expense fields, ensuring that users enter valid positive numbers.

## Contributions
Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/MorbeusDesign/MonthlyBudgetTracker/issues) for ideas on what to work on or to report bugs.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

___
If you want to contribute, feel free to do it at => 
<a href="https://www.buymeacoffee.com/Morbeus" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>
