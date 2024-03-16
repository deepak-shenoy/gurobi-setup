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

Unless specified, a variable has a zero lower bound and an infinite upper bound.  Thus the above statement really means:

```text
0 <= Cu <= 1000
```

The realities of the problem also need to be reflected.  While a dime is worth 10 cents, half a dime is not worth 5 cents.

## LP File
The Linear Programing file would resemble something like the following and placed into a file (an example can be found 
as `coins.lp` in the `cli-scripts` folder:

```text
Maximize
  .01 Pennies + 0.5 Nickels + .1 Dimes +.25 Quarters + 1 Dollars
Subject To
  Copper: .06 Pennies + 3.8 Nickles + 2.1 Dimes + 5.2 Quarters + 7.2 Dollars - Cu = 0
  Nickel: 1.2 Nickels + .2 Dimes + .5 Quarters + .2 Dollars - Ni = 0
  Zinc: 2.4 Pennies + .5 Dollars - Zi = 0
  Manganese: .3 Dollars - Mn = 0
Bounds
  Cu <= 1000
  Ni <= 50
  Zi <= 50
  Mn <= 50
Integers
  Pennies Nickels Dimes Quarters Dollars
End
```

## Running the Optimizer
Running the optimized with the LP file would follow the following example:

```text
gurobi_cl ResultFile=scratch-results/coins.sol cli-scripts/coins.lp
```

The following is an example terminal output:

```text
Set parameter Username
Set parameter LogFile to value "gurobi.log"
Using license file /Users/shenoyd/gurobi.lic

Gurobi Optimizer version 11.0.1 build v11.0.1rc0 (mac64[arm] - Darwin 23.4.0 23E214)
Copyright (c) 2024, Gurobi Optimization, LLC

Read LP format model from file cli-scripts/coins.lp
Reading time = 0.00 seconds
: 4 rows, 10 columns, 16 nonzeros

CPU model: Apple M2 Max
Thread count: 12 physical cores, 12 logical processors, using up to 12 threads

Optimize a model with 4 rows, 10 columns and 16 nonzeros
Model fingerprint: 0x70c07dbd
Variable types: 5 continuous, 5 integer (0 binary)
Coefficient statistics:
  Matrix range     [6e-02, 7e+00]
  Objective range  [1e-02, 1e+00]
  Bounds range     [5e+01, 1e+03]
  RHS range        [0e+00, 0e+00]
Found heuristic solution: objective -0.0000000
Presolve removed 1 rows and 5 columns
Presolve time: 0.00s
Presolved: 3 rows, 5 columns, 10 nonzeros
Variable types: 0 continuous, 5 integer (0 binary)
Found heuristic solution: objective 22.0000000

Root relaxation: objective 1.147436e+02, 3 iterations, 0.00 seconds (0.00 work units)

    Nodes    |    Current Node    |     Objective Bounds      |     Work
 Expl Unexpl |  Obj  Depth IntInf | Incumbent    BestBd   Gap | It/Node Time

     0     0  114.74359    0    2   22.00000  114.74359   422%     -    0s
H    0     0                     114.5000000  114.74359  0.21%     -    0s
H    0     0                     114.7000000  114.74359  0.04%     -    0s

Cutting planes:
  MIR: 1

Explored 1 nodes (3 simplex iterations) in 0.00 seconds (0.00 work units)
Thread count was 12 (of 12 available processors)

Solution count 4: 114.7 114.5 22 -0 

Optimal solution found (tolerance 1.00e-04)
Best objective 1.147000000000e+02, best bound 1.147000000000e+02, gap 0.0000%

Wrote result file 'scratch-results/coins.sol'
```

## Results

The results file 'coins.sol' would look something like the following example:

```text
# Objective value = 114.7
Pennies 0
Nickels 3
Dimes 2
Quarters 52
Dollars 100
Nickles 1.4210526315789118e+00
Cu 1000
Ni 50
Zi 50
Mn 30
```