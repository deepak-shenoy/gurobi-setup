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

### Decision Variables
The *decision variables* are what coins we need to produce
