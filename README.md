# Dataset Overview: Caravan (ISLR2)

What it is: Real customer data from a Dutch insurance company, used in the CoIL Challenge 2000. It contains sociodemographic information about 5,822 customers derived from zip codes.

Size: 5,822 observations, 86 variables

Response variable: Purchase — a binary factor (Yes/No) indicating whether the customer purchased a caravan insurance policy. Only 348 of 5,822 customers said Yes (~6%), giving you the 94/6 class imbalance we discussed.

The 85 predictors fall into three groups:

Variables starting with M — sociodemographic characteristics of the customer's zip code (income level, religion, family size, housing type, education, occupation, etc.)
Variables starting with P — number of insurance policies owned of each type (fire, car, life, boat, etc.)
Variables starting with A — number of insurance policy contributions (essentially how much they're spending on each type)

The variable names are Dutch codes, so they are cryptic, but the general structure is interpretable at that group level.
