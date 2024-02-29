# Probabilistic-Loan-Pricing
This notebook calculates the IRR of loans with final balloon payments. Model allows users to modify the price of the loan, the rates of default, interest rates, and loan life. Compares IRR to 5 year treasury rates to help bank manager determine whether to issue loan


### Using the Model

Start by loading the notebook in your preferred IDE. This code was originally developed in Google Collab

If desired, you can change the initial model data here:
```
# setting defaults
# Change the price of loan, default decay, final default, and recovery rate here. Oppurtunity to chaange interest rates and loan life later.
model_data = ModelInputs(
    price_machine = 1000000, #Set the price of loan
    loan_life = 5,
    initial_default = 0.2, #Set the initial rate of default
    default_decay = 0.9, #Set the rate that chance of default decays
    final_default = 0.4, #Set the chance of default when balloon payment becomes due
    recovery_rate = 0.4, #Set the amount of loan principle that is recovered after default. Model assumes two years of no cash flows after default
    interest_rates = 0.30,
)

model_data # prints initial data for testing
```

The model will ask you to enter interest rates and loan lives. These must be seperated by commas. If left blank or improperly formatted it will return a list of default interest rates and loan lives

```
def get_interest_rates():
    rates_str = input("Enter interest rates separated by commas (e.g., 0.30, 0.35, 0.40): ")
    if not rates_str:
      return [0.30, 0.35, 0.40]
    else:
      return [float(rate) for rate in rates_str.split(',')]

def get_loan_lives():
    lives_str = input("Enter loan lives separated by commas (e.g., 5, 10, 20): ")
    if not lives_str:
        return [5, 10, 20]
    else:
      return [int(life) for life in lives_str.split(',')]

# Get user input for interest rates and loan lives

interest_rates = get_interest_rates()
loan_lives = get_loan_lives()
```

You may adjust the number of iterations here. The model defaults to 10,000 iterations and takes the average IRR of those iterations. Raising the iterations will give more accurate results but may take longer to compute. You can lower the iterations for faster calculation.

```
# Adjust the number of iterations. More iterations gives more accurate prediction.

model_data.num_iterations = 10000 #reduce iterations for quicker execution
```

