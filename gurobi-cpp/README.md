# CPP Solution

## Example
This example is from Gurobi.

### Objective
The objective is to optimize the following model:

```text
x + y + 2z
```

Given the following constraint:

```text
x + 2y + 3z <= 4
x+y >= 1
x, y, z binary
```

### Creating the Environment and Model
The environment is created using the class `GRBEnv` and the log file name is specified by setting the environmental variable
`LogFile`.

```text
GRBEnv env = GRBEnv(true);
env.set("LogFile", "mip1.log");
env.start();
```

The environment (e.g. in this case `env`) can then be used with the Gurobi API.

The model [context] is also created through the class `GRBModel` referencing the environmental variable i.e.:

```text
GRBModel model = GRBModel(env)
```

### Setting the Variables
The variables are set within the code base using the `GRBVar` class where the ranges and types are specified:

```text
GRBVar x = model.addVar(0.0, 1.0, 0.0, GRB_BINARY, "x");
GRBVar y = model.addVar(0.0, 1.0, 0.0, GRB_BINARY, "y");
GRBVar z = model.addVar(0.0, 1.0, 0.0, GRB_BINARY, "z");
```

### Setting Constraints
Constraints are set by adding the rules to the model.  Each constraint is given a reference name:

```text
model.addConstr(x + 2 * y + 3 * z <= 4, "c0");
model.addConstr(x + y >= 1, "c1");
```

A directive is used to specify the objective i.e. maximize:

```text
model.setObjective(x + y + 2 * z, GRB_MAXIMIZE);
```

### Optimization
Once the variables, contrains and model objectives have been set the optimization process can run through the simple
execution process:

```text
model.optimize();
```

### Results
The results will be displayed at the console:

```text
Set parameter Username
Set parameter LogFile to value "mip1.log"
Gurobi Optimizer version 11.0.1 build v11.0.1rc0 (mac64[arm] - Darwin 23.4.0 23E214)

CPU model: Apple M2 Max
Thread count: 12 physical cores, 12 logical processors, using up to 12 threads

Optimize a model with 2 rows, 3 columns and 5 nonzeros
Model fingerprint: 0x98886187
Variable types: 0 continuous, 3 integer (3 binary)
Coefficient statistics:
  Matrix range     [1e+00, 3e+00]
  Objective range  [1e+00, 2e+00]
  Bounds range     [1e+00, 1e+00]
  RHS range        [1e+00, 4e+00]
Found heuristic solution: objective 2.0000000
Presolve removed 2 rows and 3 columns
Presolve time: 0.00s
Presolve: All rows and columns removed

Explored 0 nodes (0 simplex iterations) in 0.00 seconds (0.00 work units)
Thread count was 1 (of 12 available processors)

Solution count 2: 3 2 

Optimal solution found (tolerance 1.00e-04)
Best objective 3.000000000000e+00, best bound 3.000000000000e+00, gap 0.0000%
x 1
y 0
z 1
Obj: 3

Process finished with exit code 0
```

### Log File
The log file also contains the results and any associated error messages:

```text
Gurobi 11.0.1 (mac64[arm], C++) logging started Sat Mar 16 01:30:00 2024

Set parameter Username
Set parameter LogFile to value "mip1.log"
Gurobi Optimizer version 11.0.1 build v11.0.1rc0 (mac64[arm] - Darwin 23.4.0 23E214)

CPU model: Apple M2 Max
Thread count: 12 physical cores, 12 logical processors, using up to 12 threads

Optimize a model with 2 rows, 3 columns and 5 nonzeros
Model fingerprint: 0x98886187
Variable types: 0 continuous, 3 integer (3 binary)
Coefficient statistics:
  Matrix range     [1e+00, 3e+00]
  Objective range  [1e+00, 2e+00]
  Bounds range     [1e+00, 1e+00]
  RHS range        [1e+00, 4e+00]
Found heuristic solution: objective 2.0000000
Presolve removed 2 rows and 3 columns
Presolve time: 0.00s
Presolve: All rows and columns removed

Explored 0 nodes (0 simplex iterations) in 0.00 seconds (0.00 work units)
Thread count was 1 (of 12 available processors)

Solution count 2: 3 2 

Optimal solution found (tolerance 1.00e-04)
Best objective 3.000000000000e+00, best bound 3.000000000000e+00, gap 0.0000%

Gurobi 11.0.1 (mac64[arm], C++) logging started Sat Mar 16 21:14:24 2024

Set parameter Username
Set parameter LogFile to value "mip1.log"
Gurobi Optimizer version 11.0.1 build v11.0.1rc0 (mac64[arm] - Darwin 23.4.0 23E214)

CPU model: Apple M2 Max
Thread count: 12 physical cores, 12 logical processors, using up to 12 threads

Optimize a model with 2 rows, 3 columns and 5 nonzeros
Model fingerprint: 0x98886187
Variable types: 0 continuous, 3 integer (3 binary)
Coefficient statistics:
  Matrix range     [1e+00, 3e+00]
  Objective range  [1e+00, 2e+00]
  Bounds range     [1e+00, 1e+00]
  RHS range        [1e+00, 4e+00]
Found heuristic solution: objective 2.0000000
Presolve removed 2 rows and 3 columns
Presolve time: 0.00s
Presolve: All rows and columns removed

Explored 0 nodes (0 simplex iterations) in 0.00 seconds (0.00 work units)
Thread count was 1 (of 12 available processors)

Solution count 2: 3 2 

Optimal solution found (tolerance 1.00e-04)
Best objective 3.000000000000e+00, best bound 3.000000000000e+00, gap 0.0000%
```