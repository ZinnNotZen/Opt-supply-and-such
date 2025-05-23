## Optimization Model for Cargo Shipping
# Overview
This project implements a linear optimization model to minimize the total cost of shipping cargo from supply hubs to fulfillment centers while satisfying supply, demand, and non-negativity constraints. The model uses Python and PuLP to formulate and solve the capacitated transportation problem.

# Model Analysis and Results
Solution Optimality and Constraint Satisfaction
The solver returned a status of "Optimal", confirming that all constraints were satisfied.

Supply constraints: The total cargo shipped from each supplier did not exceed its available monthly capacity.

Demand constraints: The demand for each fulfillment center was met exactly as specified.

Non-negativity constraints: All shipping quantities were zero or positive.

# Key Output
Only one shipment was needed in this scenario:

AFW -> Austin: 1900.00 tons

This confirms that the supply capacity at AFW and the demand at Austin were handled without violating any constraints.

# Model Components
Decision Variables:
xij represents the quantity of cargo shipped from supplier i to fulfillment center j.
Implemented with PuLP’s LpVariable.dicts.

# Constraints:

Supply constraints ensure shipments from each hub/focus city do not exceed capacity.

Demand constraints ensure the fulfillment center demands are met.

Non-negativity constraints (enforced by lowBound=0 in variables).

# Objective Function:
Minimize total shipping cost = sum over all (cost_per_ton * tons_shipped).
Implemented using PuLP’s lpSum().

Why the Output Matches Expectations
Cost data were realistic, and supply/demand values were feasible for at least one shipping route.

The route AFW to Austin had a low shipping cost and could fulfill the entire demand without exceeding supply.

Because the test scenario included only one demand point and sufficient supply, the model’s single-route solution minimizes cost while satisfying all constraints.

# Reflection on Development Process
The modeling logic — defining variables, setting constraints, and minimizing cost — was conceptually straightforward.

Implementation challenges arose from improper data formatting:

Initially, passing entire Pandas Series caused recursive evaluation errors.

Refactoring data into clean Python dictionaries for supply, demand, and cost resolved these issues.

The model was initially infeasible when all constraints were strictly enforced, likely due to combined demand exceeding supply or missing cost data for some routes.

Introducing a small relaxation (epsilon buffer of 0.3) allowed the solver to find a solution, but it was trivial (no shipments).

This experience highlighted the importance of:

Validating assumptions and data early.

Understanding solver errors and model feasibility.

Iterative debugging and refining the model setup.

The final working solution gave confidence that the model is correct, complete, and ready for further extension.

# Usage
Ensure Python and PuLP are installed.

Provide input data as Python dictionaries for supply, demand, and cost.

Run the optimization script to get shipment quantities and total cost.

Review solver status to confirm optimality and constraint satisfaction.
