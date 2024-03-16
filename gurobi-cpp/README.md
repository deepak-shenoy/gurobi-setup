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