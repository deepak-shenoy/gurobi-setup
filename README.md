# Gurobi Setup
 In order to formulate an optimization problem the following things are needed:
 
1. Defining the correct decision variables that represent the problem.
2. Define a linear objective function (this is a function that helps us minimize or maximize the result space).
3. Linear constraints

### Sample problem
If we have a limited supply of metals, what is the greatest dollar value of 
coins that can be created from those materials?

| Material    | Penny | Nickle | Dime | Quarter | Dollar |
|:------------|:------|:------|:-----|:--------|:------|
| Copper (Cu) | 0.06g | 3.8g  | 2.1g | 5.2g    | 7.2g  |
| Nickel (Ni) |       | 1.2g  | 0.2g | 0.5g    | 0.2g  |
| Zinc (Zi)   | 2.4g  |       |      |         |0.5g|
|Manganese (Mn)|    |     |      |      |0.3g|

### Decision Variables and Constraints
The **decision variables** are what coins we need to produce: Pennies, 
Nickles, Dimes, Quarters and Dollars

This then defines our linear objective:

```text
maximize: 0.01 Pennies + 0.05 Nickles + 0.1 Dimes + 0.25 Quarters + 1 Dollars
```

The constraints of this model represent that creating a coin will consume certain quantities of the
metals.  For example, the breakdown of how copper would be used would look like the following:

```text
Cu = 0.06 Pennies + 3.8 Nickles + 2.1 Dimes + 5.2 Quarters + 7.2 Dollars
```

The coefficients define how much of each material a specific coin type will use.  For example, a Penny would use 0.06g
of copper and one Nickle uses 3.8g of copper.

### Constraints
For our example, if we assume that we have 1000 grams of copper and 50 grams of other materials we can define the following
constraint for copper:

```text
Cu <= 1000
```
The realities of the problem also need to be reflected.  While a dime is worth 10 cents, half a dime is not worth 5 cents.