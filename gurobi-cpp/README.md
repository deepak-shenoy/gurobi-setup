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

### Creating the Environment
The environment is created using the class `GRBEnv` and the log file name is specified by setting the environmental variable
`LogFile`.

```text
GRBEnv env = GRBEnv(true);
env.set("LogFile", "mip1.log");
env.start();
```

The environment (e.g. in this case `env`) can then be used with the Gurobi API.

### Setting the Variables
