# Investment Calculator

An investment calculator built using React.js that helps users calculate the future value of their investments. The calculator allows users to input initial investment, annual investment, expected return rate, and investment duration. Additionally, users can choose between USD and INR as the currency for their calculations.

## Features

- Input fields for initial investment, annual investment, expected return, and duration.
- Currency selector to choose between USD and INR.
- Results table displaying the year-by-year investment value, interest earned, total interest, and invested capital.

## Installation

To run this project locally, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/SmitParekh84/Investment-Calculator.git
    cd investment-calculator
    ```

2. Install the dependencies:
    ```bash
    npm install
    ```

3. Start the development server:
    ```bash
    npm start
    ```

The application will be available at `http://localhost:3000`.

## Usage

1. Open the application in your web browser.
2. Fill in the input fields with your initial investment, annual investment, expected return, and duration.
3. Select the currency (USD or INR) from the dropdown.
4. The results table will automatically update, displaying the investment value, interest earned, total interest, and invested capital for each year.

## Project Structure

- `src/components/`
  - `Header.jsx`: The header component.
  - `UserInput.jsx`: The component for user inputs.
  - `Results.jsx`: The component for displaying the results.
- `src/util/`
  - `investment.js`: Contains the investment calculation logic and currency formatter function.
- `src/App.jsx`: The main app component.

## Code Overview

### investment.js

Contains the `calculateInvestmentResults` function to compute the investment results based on the user input and the `getFormatter` function to format the numbers according to the selected currency.

```javascript
export function calculateInvestmentResults({
  initialInvestment,
  annualInvestment,
  expectedReturn,
  duration,
}) {
  const annualData = [];
  let investmentValue = initialInvestment;

  for (let i = 0; i < duration; i++) {
    const interestEarnedInYear = investmentValue * (expectedReturn / 100);
    investmentValue += interestEarnedInYear + annualInvestment;
    annualData.push({
      year: i + 1,
      interest: interestEarnedInYear,
      valueEndOfYear: investmentValue,
      annualInvestment: annualInvestment,
    });
  }

  return annualData;
}

export function getFormatter(currency) {
  const locale = currency === 'USD' ? 'en-US' : 'en-IN';
  return new Intl.NumberFormat(locale, {
    style: 'currency',
    currency: currency,
    minimumFractionDigits: 0,
    maximumFractionDigits: 0,
  });
}
