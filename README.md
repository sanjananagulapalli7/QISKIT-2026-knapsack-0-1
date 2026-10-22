# QISKIT-2026-knapsack-0-1
1) Background: From classical to quantum computing.

  1.1 ) what is an optimization problem?
An optimization problem involves finding the best possible solution from a set of possible choices while satisfying specified constraints. The goal may be to maximize a quantity, such as profit or value, or minimize a quantity, such as cost, time, or energy consumption.
Optimization problems arise in many real-world applications, including transportation, logistics, resource allocation, scheduling, and supply chain management.
Most optimization problems can be described using three key components:
- Decision variables: The choices we can make.
- Objective function: The mathematical expression describing what we want to maximize or minimize.
- Constraints: The rules or limitations that a valid solution must satisfy.
  
  1.2) How Do Classical Computers Solve Optimization Problems?
Classical computers process information using bits, which represent either 0 or 1. They use logical operations and algorithms to perform calculations, evaluate possible solutions, and solve optimization problems.
Depending on the problem, a classical algorithm may examine possible solutions individually, use mathematical techniques to find an exact answer, or apply heuristics to find a good solution without checking every possibility.
For small optimization problems, exhaustive search can be an effective approach. It evaluates every possible selection and identifies the best valid solution. However, the number of possible selections can grow exponentially as the number of decision variables increases.
For example, if a problem has (n) binary decision variables, there are (2^n) possible assignments. This means that adding more decision variables can make exhaustive search increasingly expensive.
Classical computers remain highly effective for many optimization problems. The difficulty of solving a particular problem depends on its structure, size, and the algorithm used.

  1.3) Why Investigate Quantum Computing?
Although classical computers solve many optimization problems effectively, some problem classes become computationally expensive as their size increases. This has motivated researchers to investigate alternative computational approaches, including quantum computing.
Quantum computers use principles of quantum mechanics to represent and process information. Unlike classical bits, which represent either 0 or 1, quantum bits (qubits) can exist in quantum superpositions of the states represented by 0 and 1.
Quantum algorithms use quantum operations to manipulate these states and can produce measurement outcomes whose probabilities depend on the computation performed. For certain problems, carefully designed quantum algorithms may offer advantages over the best known classical approaches.
However, quantum computers are not universally faster than classical computers. Any practical advantage depends on the problem, the algorithm, the hardware, and the performance of the available classical methods. Current quantum processors are also affected by noise and hardware limitations.
This project investigates a quantum optimization approach to understand its behavior under specified processor configurations, rather than assuming that quantum computing will automatically outperform classical methods.

  1.4)What Is a Quantum Processor?
A quantum processor is a physical computing device that uses controllable quantum systems to perform quantum operations. Its basic units of quantum information are called qubits.
A quantum algorithm is expressed as a sequence of quantum operations, commonly represented as a quantum circuit. The processor applies these operations to its qubits, changes their quantum states, and measures the resulting states to produce classical data.
A quantum processor does not independently decide which solution to choose. The algorithm defines the computation, while the processor executes the corresponding quantum operations. A classical computer typically works alongside it to prepare inputs, optimize algorithm parameters, process measurement results, and evaluate performance.
The capabilities of a quantum processor depend on several factors, including its number of qubits, the connections between qubits, the operations it supports, and the errors that occur during computation and measurement.
Consequently, evaluating a quantum algorithm requires considering not only its mathematical design but also how well it can be implemented on the target processor.

  1.5) Quantum Computing for Optimization
Quantum optimization is an area of research that investigates how quantum algorithms can be used to find high-quality solutions to optimization problems.
One approach is the Quantum Approximate Optimization Algorithm (QAOA). QAOA combines parameterized quantum circuits with classical optimization: a quantum circuit generates measurement outcomes, and a classical optimizer uses information from those outcomes to adjust the circuit parameters.
The objective is to increase the likelihood of obtaining good solutions while respecting the problem's constraints. The quality of the results depends on the mathematical formulation, circuit structure, parameter choices, processor characteristics, and noise.
In this project, we investigate QAOA for the 0/1 Knapsack Problem specified in Qiskit Fall Fest 2026, Problem Statement PS-O3. We will compare the specified Processor A and Processor B configurations to examine how their connectivity and resulting circuit implementations affect solution quality and hardware-related metrics.
Because the problem is small enough to solve exactly using a classical computer, we can establish a classical reference solution and evaluate the quantum results against it. This allows us to investigate the behavior and limitations of the approach without assuming that quantum computing provides a practical advantage.

 2) Understanding Quantum Processors
A quantum processor executes quantum circuits using physical qubits and quantum operations. To understand how processor hardware affects our optimization experiments, we first need to understand how qubits represent information, how quantum gates manipulate that information, and how measurements produce results.
The processor's qubit count, connectivity, supported operations, and error characteristics can all influence how a quantum algorithm is implemented and how well it performs.
 2.1) Qubits and Superposition
A qubit, or quantum bit, is the basic unit of quantum information. Unlike a classical bit, which can represent either 0 or 1, a qubit can exist in a quantum superposition of the states associated with these two values.
The state of a qubit can be represented mathematically as:
$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$
This equation is read as: "The quantum state psi equals alpha times the zero state plus beta times the one state."
Here is what each symbol means:
- Psi ($\psi$): Represents the overall quantum state of the qubit.
- Alpha ($\alpha$): The probability amplitude associated with measuring 0.
- Beta ($\beta$): The probability amplitude associated with measuring 1.
- $|0\rangle$ and $|1\rangle$: The two computational basis states, representing the possible measurement outcomes 0 and 1.
Alpha and beta are amplitudes, not probabilities themselves. The probabilities are calculated by taking the squared magnitudes of the amplitudes.
The normalization condition is:
$$
|\alpha|^2 + |\beta|^2 = 1
$$
This means that the probabilities of measuring 0 and 1 must add up to 1, or 100%.
The probability of measuring 0 is:
$$
P(0) = |\alpha|^2
$$
The probability of measuring 1 is:
$$
P(1) = |\beta|^2
$$
For example, suppose both amplitudes equal one divided by the square root of two:
$$
\alpha = \frac{1}{\sqrt{2}},
\qquad
\beta = \frac{1}{\sqrt{2}}
$$
Squaring each amplitude gives:
$$
P(0) = \left|\frac{1}{\sqrt{2}}\right|^2
= \frac{1}{2} = 50%
$$
$$
P(1) = \left|\frac{1}{\sqrt{2}}\right|^2
= \frac{1}{2} = 50%
$$
Therefore, the qubit has a 50% probability of producing 0 and a 50% probability of producing 1 when measured in the computational basis.
Superposition is an important feature of quantum computing. However, measuring a qubit does not reveal all possible states simultaneously. Quantum algorithms use carefully designed operations and quantum interference to influence the probabilities of measurement outcomes.
2.2) Quantum Gates
A quantum gate is an operation that changes the state of one or more qubits. Quantum gates are the building blocks of a quantum circuit, just as logic operations are building blocks of classical computing.
Different gates perform different operations. Some change a qubit's state, while others create relationships between qubits. By applying gates in a carefully chosen sequence, a quantum algorithm can control how a quantum system evolves.
Some important quantum gates include:
- X gate: Flips the computational basis states: 0 becomes 1, and 1 becomes 0.
- Hadamard gate (H): Creates an equal superposition when applied to the basis state 0 or 1.
- RZ gate: Rotates the qubit's state around the Z axis of the Bloch sphere.
- SX gate: Performs a square-root-of-X operation.
- CNOT gate (CX): A two-qubit gate that flips the target qubit when the control qubit is 1.
The gates available on a quantum processor depend on its hardware and supported operations. A circuit may need to be rewritten using the gates supported by the target processor before it can run.
In this project, the specified native gate set is RZ, SX, X, and CX. We will later examine how these gates are used to implement QAOA and how the processor's connectivity can affect the resulting circuit.
2.3)Qubit Connectivity
Qubit connectivity describes which pairs of qubits can directly interact through two-qubit gates on a quantum processor.
A quantum processor may contain several qubits, but that does not mean every qubit can directly interact with every other qubit. The available connections depend on the processor's hardware architecture.
For example, suppose a processor has three qubits: 0, 1, and 2.
If its available connections are (0, 1) and (1, 2), qubit 0 can directly interact with qubit 1, and qubit 1 can directly interact with qubit 2. However, qubits 0 and 2 do not have a direct connection.
When a quantum circuit requires two qubits without a direct connection to interact, the circuit may need additional operations, such as SWAP gates, to move quantum information between connected qubits.
These extra operations can increase circuit depth and gate count. On noisy quantum hardware, additional gates may also increase the likelihood of errors.
In this project, we compare two specified processor layouts:
- Processor A: 5 physical qubits with 4 listed connections.
- Processor B: 9 physical qubits with 12 listed connections.
Our knapsack problem contains 5 decision variables, so we must investigate how the two processor layouts affect circuit implementation, gate count, SWAP overhead, circuit depth, and solution quality.
A larger number of connections does not automatically guarantee better results. The actual outcome depends on the circuit, the mapping of logical qubits to physical qubits, the compilation process, and noise.
2.4) Circuit Depth and Gate Count
A quantum circuit is a sequence of quantum gates applied to qubits. Two important measurements used to describe a circuit are gate count and circuit depth.
Gate count is the total number of gates used in a circuit. We can also count specific types of gates separately, such as CX gates and SWAP gates.
Circuit depth describes the number of sequential layers of operations needed to execute a circuit. Gates acting on separate qubits may sometimes run in parallel, while gates that depend on earlier operations must run in later layers.
For example, consider two gates acting on two different qubits. If neither gate depends on the other, they may be executed in the same layer. If one gate must finish before another can begin, they belong to different layers.
A circuit with more gates does not necessarily have greater depth, because some gates can execute in parallel.
Circuit depth matters because a deeper circuit may take longer to execute and may be more affected by noise. However, actual execution time and error rates also depend on the hardware and the operations being performed.
In our project, we will compare the compiled circuits for Processors A and B using metrics such as:
- Total gate count.
- Number of CX gates.
- Number of SWAP gates introduced during compilation.
- Circuit depth.
- Number of physical qubits used.
These measurements will help us understand how processor connectivity and circuit compilation affect the implementation of QAOA for the knapsack problem.
2.5 Quantum Noise and Errors
Quantum processors are affected by noise, which can cause their actual behavior to differ from the ideal behavior expected from a quantum circuit.
Unlike an ideal simulation, a real quantum processor cannot perform every operation perfectly. Errors may occur while gates are being applied or while qubits are being measured.
Two important sources of error in our project are depolarizing error and readout error.
Depolarizing error is a noise model that represents the possibility of a quantum operation disturbing the intended quantum state. In our experiments, separate depolarizing error rates are specified for single-qubit gates and two-qubit CX gates.
Readout error occurs when a qubit is measured but the recorded result differs from the outcome that the measurement should have produced. For example, a qubit whose measurement outcome should be recorded as 0 may instead be recorded as 1.
Noise can affect the measured distribution of solutions. As a result, the most frequently measured answer may differ from the ideal result, and the probability of obtaining an optimal or valid solution may decrease.
To compare Processor A and Processor B fairly, we will use the same specified synthetic noise rates for both processors. This helps us investigate how their connectivity and compiled circuits affect performance under a consistent noise model.
We will distinguish between ideal simulation results and noisy simulation results. This distinction is important because an ideal simulation does not include the effects of the specified noise model.
The exact noise rates, simulation settings, and experimental procedure will be documented in the experiment configuration section of this README.
2.6 Quantum Measurement
Quantum measurement converts the information represented by a quantum state into a classical result that a computer can record and analyze.
Before measurement, a qubit may be in a superposition of the states associated with 0 and 1. When measured in the computational basis, it produces one classical outcome: either 0 or 1. The outcome is probabilistic when the quantum state does not correspond to a definite measurement result.
For a circuit containing multiple qubits, measurement produces a bit string, such as "10100". Each bit represents the recorded outcome of a measured qubit.
Quantum algorithms are often executed repeatedly to collect measurement results. Each execution is called a shot. For example, running a circuit for 4,096 shots produces 4,096 measurement outcomes.
The outcomes can be grouped into a count distribution. If a bit string appears frequently, it has a higher observed frequency in that experiment. However, a frequently measured result is not necessarily the optimal solution.
In our knapsack problem, each bit represents whether an item is selected:
- "1" means the item is selected.
- "0" means the item is not selected.
We will analyze the measurement counts to determine how often the circuit produces feasible solutions and how often it produces the optimal solution. A feasible solution satisfies the knapsack's capacity constraint, while the optimal solution is the feasible selection with the highest total value.
Measurement results are therefore essential for evaluating QAOA. They connect the behavior of a quantum circuit to the practical quality of the solutions it produces.
 3) The 0/1 Knapsack Problem
The 0/1 Knapsack Problem is a classical combinatorial optimization problem. It involves selecting items to maximize their total value without exceeding a specified weight capacity.
The problem is called "0/1" knapsack because each item has only two possible decisions: either it is selected or it is not selected. Items cannot be partially selected.
This problem appears in many real-world situations, including budget allocation, cargo loading, project selection, and resource management. In each case, limited resources must be allocated to obtain the greatest possible benefit.
In Qiskit Fall Fest 2026, Problem Statement PS-O3 asks us to investigate how the Quantum Approximate Optimization Algorithm (QAOA) can be applied to the 0/1 Knapsack Problem.
Our task is not simply to find a good selection of items. We must also investigate how the problem can be represented for a quantum algorithm, how the algorithm performs on two specified processor layouts, and how circuit compilation and noise affect the results.
Because this is a small problem, we can calculate the exact classical optimum and use it as a reference when evaluating our quantum experiments.
3.1 Problem Data
The knapsack problem specifies five items, each with a value and a weight. The total weight of the selected items must not exceed the knapsack's capacity.
The given capacity is 15 weight units.
Item| Value| Weight
A| 10| 5
B| 4| 3
C| 7| 4
D| 5| 2
E| 8| 6
The values represent the benefit obtained from selecting each item, while the weights represent the resources consumed.
The decision for each item is binary:
- "1" means the item is selected.
- "0" means the item is not selected.
Since there are five items and each has two possible decisions, the total number of possible selections is:
$$
2^5 = 32
$$
In other words, there are 32 possible combinations of selected and unselected items. Some combinations satisfy the capacity constraint, while others exceed it.
Because all 32 combinations can be evaluated by a classical computer, we can use exhaustive search to establish the exact optimum. This gives us a reliable reference for assessing the solutions obtained from QAOA.
3.2) Classical Reference Solution
Before evaluating QAOA, we need to establish the exact optimal solution using a classical method. This provides a reference against which the quantum results can be compared.
For this problem, the optimal selection is:
Select items A, B, C, and D. Do not select item E.
We can represent this selection using a binary decision vector, where each position corresponds to an item in the order A, B, C, D, E:
"11110"
Here, "1" indicates that an item is selected, and "0" indicates that it is not selected.
The total weight of the selected items is:
$$
5 + 3 + 4 + 2 = 14
$$
The total value is:
$$
10 + 4 + 7 + 5 = 26
$$
The capacity constraint is satisfied because the total weight is 14, which does not exceed the capacity of 15.
The total value of 26 is the highest possible among all feasible selections. We can verify this by evaluating all 32 possible selections using exhaustive search.
Therefore, the classical reference solution has:
- Selected items: A, B, C, D
- Total weight: 14
- Total value: 26
- Unused capacity: 1 weight unit
- Binary decision vector (A–E order): "11110"
This result is our benchmark. Our quantum experiments do not need to rediscover the reference solution perfectly in every shot, but we will measure how frequently they produce it and how their overall solution quality compares with the classical optimum.
3.3) Decision Variables and Objective
To express the knapsack problem mathematically, we assign one binary decision variable to each item.
Let "x_A", "x_B", "x_C", "x_D", and "x_E" represent the decisions for items A, B, C, D, and E.
Each variable can take only one of two values:
- "1" if the corresponding item is selected.
- "0" if the corresponding item is not selected.
The objective is to maximize the total value of the selected items.
Using the values provided in the problem statement, the objective function is:
$$
V = 10x_A + 4x_B + 7x_C + 5x_D + 8x_E
$$
Here, "V" is the total value. Each coefficient is the value of its corresponding item, and each binary variable determines whether that value contributes to the total.
For example, selecting A, B, C, and D while leaving E unselected gives:
$$
V = 10(1) + 4(1) + 7(1) + 5(1) + 8(0) = 26
$$
The selection must also satisfy the capacity constraint:
$$
5x_A + 3x_B + 4x_C + 2x_D + 6x_E \leq 15
$$
In this expression, each coefficient is an item's weight. The sum represents the total weight of the selected items, which must be no greater than 15.
Together, the objective function and capacity constraint define the original 0/1 Knapsack Problem: maximize total value while keeping total weight within the available capacity.
3.5) Why Do We Need a Mathematical Encoding?
The original knapsack problem is expressed using binary decisions, an objective function, and a capacity constraint. However, a quantum circuit does not directly understand a problem statement written in ordinary language.
To use QAOA, we must translate the optimization problem into a mathematical form that can be represented by quantum operations.
One common approach is to express the objective using binary variables and then convert it into a quadratic unconstrained binary optimization (QUBO) model. A QUBO model expresses the cost of a selection using binary variables and terms involving products of pairs of variables.
The term unconstrained means that the capacity constraint is no longer written as a separate restriction in the final QUBO expression. Instead, violations must be discouraged through an appropriate penalty construction or handled using another valid encoding.
This step requires care. If the penalty is poorly designed, the model may favor invalid selections or change which solution is optimal.
After constructing and validating the mathematical model, we can convert it into an Ising representation suitable for a quantum optimization circuit. QAOA then uses this representation to build parameterized quantum operations and search for good solutions.
We will derive the encoding step by step rather than assume that a particular penalty formula is correct. The encoded model must preserve the original problem's intended optimum before its quantum performance can be evaluated.
3.6) What Is QUBO?
QUBO stands for Quadratic Unconstrained Binary Optimization.
Each word describes a property of the mathematical model:
- Quadratic: The objective can contain products of two binary variables, such as "x_A × x_B".
- Unconstrained: The model expresses the optimization objective without separate hard constraints. Any original constraints must be handled appropriately within the objective or through the encoding.
- Binary: Every decision variable can take only the value 0 or 1.
- Optimization: The goal is to find the variable assignment that gives the best objective value.
A general QUBO objective can be written as:
$$
E(x) = \sum_i Q_{ii}x_i
+ \sum_{i<j} Q_{ij}x_i x_j
$$
Here, "E(x)" is the objective value being minimized, "x_i" is the binary decision for variable "i", and "Q" contains the numerical coefficients that define the model.
The first sum contains individual-variable terms. The second sum contains pairwise interaction terms. Because the variables are binary, each variable can only be 0 or 1.
For our knapsack problem, the original objective is to maximize total item value while respecting the capacity limit. A QUBO model must encode this goal and handle the capacity restriction so that the intended optimal selection remains optimal under the encoded objective.
Important: QUBO objectives are commonly written as minimization problems. Since our original problem maximizes value, we must account for that direction when constructing the QUBO. We must also validate any penalty coefficients instead of choosing them arbitrarily.
We will derive the actual knapsack QUBO only after establishing a mathematically sound way to handle the capacity constraint.
3.7) Handling the Capacity Constraint
Our original knapsack problem has a hard capacity constraint: the total weight of selected items must not exceed 15.
A QUBO objective does not use a separate hard constraint in its standard form. We therefore need a way to discourage selections that violate the capacity limit.
One common approach is to add a penalty term to the objective. The penalty makes invalid selections less attractive by increasing their cost.
However, we must design this penalty carefully. A penalty that is too small may allow an overweight selection to win. A penalty that is too large may create unnecessarily large differences between objective values, which can make optimization more difficult.
There is also an important mathematical detail: simply penalizing the difference between the capacity and the selected weight can be incorrect. A selection that leaves unused capacity is not invalid, so unused capacity must not automatically be treated as a violation.
For this reason, we must distinguish between:
- Valid selections: Their total weight is at most 15.
- Invalid selections: Their total weight exceeds 15.
- Penalty design: The mathematical construction must discourage invalid selections without incorrectly penalizing valid ones.
A standard way to convert an inequality constraint into an equality is to introduce additional binary variables representing unused capacity. These are called slack variables. The resulting model can then penalize violations of the equality.
For our five-item problem, we will derive the slack-variable encoding, determine the required coefficients, and verify the encoded objective against all 32 possible item selections before using it in QAOA.
3.8)What Are Slack Variables?
Slack variables help convert an inequality constraint into an equality constraint.
In our knapsack problem, the total selected weight can be less than 15. The difference between the capacity and the selected weight is the unused capacity.
We can represent this unused capacity using a new variable called a slack variable, represented by "s".
The capacity constraint is:
$$
5x_A + 3x_B + 4x_C + 2x_D + 6x_E \leq 15
$$
Introducing the slack variable converts it into:
$$
5x_A + 3x_B + 4x_C + 2x_D + 6x_E + s = 15
$$
Here, "s" represents the unused capacity. It must be a non-negative integer for this problem.
For example, the classical optimal selection A, B, C, and D has total weight 14. Its unused capacity is therefore:
$$
s = 15 - 14 = 1
$$
The equality becomes:
$$
14 + 1 = 15
$$
To represent every possible integer slack value from 0 to 15 using binary variables, we can use four additional bits with weights 1, 2, 4, and 8.
This introduces an important trade-off for our project. The five item decisions already require five logical qubits. A binary representation of the slack variable adds four more, making nine logical qubits in total.
Processor A has five physical qubits, while Processor B has nine. Therefore, this encoding fits within Processor B's qubit count but does not fit directly on Processor A without a different encoding or approach.
We must account for this limitation when choosing and comparing our mathematical formulations. The formulation must represent the original knapsack problem correctly and remain compatible with the hardware constraints of the processors being studied.
3.9) Constructing the Knapsack QUBO
We want to maximize the total value of the selected items while ensuring that their total weight does not exceed 15.
QUBO is conventionally written as a minimization problem. Therefore, we express the value objective as a negative quantity so that maximizing value is equivalent to minimizing negative value.
The negative-value objective is:
$$
-V = -(10x_A + 4x_B + 7x_C + 5x_D + 8x_E)
$$
We then introduce four binary slack variables, "s₀", "s₁", "s₂", and "s₃", to represent unused capacity.
Their combined value is:
$$
s = s_0 + 2s_1 + 4s_2 + 8s_3
$$
Each slack variable can take the value 0 or 1. Together, they represent integer values from 0 to 15.
We can now express the capacity constraint as an equality:
$$
5x_A + 3x_B + 4x_C + 2x_D + 6x_E
+ s_0 + 2s_1 + 4s_2 + 8s_3 = 15
  $$
To encourage this equality to hold, we add a squared penalty to the negative-value objective:
$$
\begin{aligned}
E(x,s) ={}&
-(10x_A + 4x_B + 7x_C + 5x_D + 8x_E)\
&+\lambda\big(
5x_A + 3x_B + 4x_C + 2x_D + 6x_E\
&\qquad +s_0+2s_1+4s_2+8s_3-15
\big)^2
\end{aligned}
$$
Here, "E(x,s)" is the QUBO energy that we want to minimize, and "λ" (lambda) is the penalty coefficient. When the equality is satisfied, the penalty is zero. When it is violated, the squared term increases the energy.
The penalty coefficient must be large enough to prevent an invalid selection from becoming preferable to the true optimum. We will derive and verify a suitable value rather than choose one arbitrarily.
This formulation uses five item variables and four slack variables, giving nine binary variables in total. It is therefore compatible with a nine-qubit representation in principle, although the compiled circuit must still be checked against the processor's connectivity and supported gates.
Before using this model in QAOA, we must verify that its minimum corresponds to the classical optimal selection, A, B, C, and D, with total value 26 and total weight 14.
3.10 )Choosing the Penalty Coefficient
In our QUBO formulation, the penalty coefficient, "λ" (lambda), determines how strongly the model discourages violations of the capacity equality.
If the penalty is too small, an overweight selection with a high value might have a lower energy than the correct solution. If the penalty is sufficiently large, every infeasible selection will have a higher energy than the classical optimum.
We can derive a sufficient lower bound for this particular problem.
The total value of all five items is:
$$
10 + 4 + 7 + 5 + 8 = 34
$$
The classical optimal value is 26. Therefore, even the highest-value selection can exceed the optimal value by at most:
$$
34 - 26 = 8
$$
For any infeasible selection, the capacity equality cannot be satisfied by the available slack variables. Because all weights and slack values are integers, the absolute difference in the equality is at least 1. Its squared penalty is therefore at least "λ".
To ensure that every infeasible selection has a higher energy than the optimal feasible selection, we require:
$$
-34 + \lambda > -26
$$
Rearranging gives:
$$
\lambda > 8
$$
Thus, any penalty coefficient strictly greater than 8 is sufficient under this formulation. For example, "λ = 9" satisfies this bound.
This is a mathematically derived starting choice, not an experimentally optimized parameter. Before accepting it, we must verify the encoded objective by enumerating the binary assignments and checking that its minimum corresponds to the classical optimum.
We must also distinguish between two questions: whether the mathematical model is correct and whether QAOA can find its minimum efficiently. A correct encoding does not guarantee that a finite-depth, noisy quantum circuit will frequently measure the optimal solution.
3.11) Validating the QUBO Formulation
Before using the QUBO model in QAOA, we must verify that it preserves the original knapsack problem's optimal solution.
Our formulation contains five item variables and four slack variables. Since each variable is binary, the total number of assignments to evaluate is:
$$
2^9 = 512
$$
This gives us a small enough search space to check exhaustively using a classical computer.
We will validate the formulation using the following procedure:
1. Enumerate all 512 assignments of the five item variables and four slack variables.
2. Calculate the total weight and total value for each item selection.
3. Calculate the slack value represented by the four slack bits.
4. Evaluate the QUBO energy using the selected penalty coefficient.
5. Identify the minimum energy and compare its item selection with the classical reference solution.
6. Confirm that the minimum-energy solution selects items A, B, C, and D, with total weight 14 and total value 26.
We must also verify that the penalty correctly distinguishes feasible and infeasible item selections. Every feasible selection must be representable by an appropriate slack assignment, while an infeasible selection must be unable to satisfy the capacity equality.
This classical validation is separate from running QAOA. It checks the mathematical encoding itself, whereas QAOA experiments evaluate how effectively a parameterized quantum circuit can find low-energy solutions.
We will treat the formulation as validated only after the implementation passes these checks. The verification results and relevant tests will be documented alongside the experimental code to support reproducibility.
4) The Quantum Approximate Optimization Algorithm (QAOA)
The Quantum Approximate Optimization Algorithm, commonly called QAOA, is a hybrid quantum-classical algorithm designed for combinatorial optimization problems.
The word hybrid means that the algorithm uses both a quantum processor or simulator and a classical computer. The quantum circuit generates measurement outcomes, while a classical optimizer adjusts the circuit's parameters to improve the results.
QAOA does not guarantee that every execution will produce the optimal solution. Instead, it aims to increase the probability of obtaining good solutions by repeatedly preparing and evaluating a parameterized quantum circuit.
In our project, QAOA will be used to investigate the 0/1 Knapsack Problem from PS-O3. We will study how the mathematical encoding, circuit structure, processor connectivity, and noise affect its performance.
The main stages of QAOA are:
1. Encode the optimization problem into a suitable mathematical objective.
2. Construct a parameterized quantum circuit based on that objective.
3. Execute the circuit and collect measurement outcomes.
4. Evaluate the outcomes using a classical computer.
5. Use a classical optimizer to update the circuit parameters.
6. Repeat the process until the chosen stopping condition is reached.
The final measurement distribution can then be analyzed to determine how frequently the circuit produces feasible solutions and how often it finds the classical optimum.
Throughout this project, we will distinguish between the mathematical correctness of our encoding, the optimization behavior of QAOA, and the effects of processor compilation and noise. These are related, but they measure different aspects of the experiment.
4.1) Preparing the Initial State
QAOA begins by preparing the qubits in an initial quantum state. A common choice is to place every qubit into an equal superposition of its two computational basis states.
For a single qubit, a Hadamard gate applied to the state 0 creates an equal superposition of 0 and 1.
For a circuit with multiple qubits, applying a Hadamard gate to each qubit creates a superposition over all possible binary strings.
Our knapsack problem has five item decision variables. Considering only these five variables, the number of possible selections is:
$$
2^5 = 32
$$
An equal-superposition initial state assigns equal measurement probability to these 32 selections before the QAOA problem-dependent operations are applied.
If we use the nine-variable slack formulation described earlier, the initial state instead covers:
$$
2^9 = 512
$$
possible binary assignments.
The choice of variables therefore affects the size of the quantum state and the number of qubits required. We must account for this when designing a formulation that can be implemented on the specified processors.
Preparing an equal superposition does not itself identify the optimal selection. It provides an initial state from which QAOA's subsequent operations can influence the measurement probabilities.
4.2 )The Cost Layer
The cost layer encodes the optimization objective into quantum operations. Its purpose is to make the quantum circuit respond differently to different candidate solutions according to their objective values.
For our knapsack problem, the original objective is to maximize the total value of selected items while respecting the capacity constraint. In the QUBO formulation, we express this as minimizing an energy function that includes both the negative item value and the constraint penalty.
The cost layer uses the encoded objective to apply phase changes to the quantum state. These phase changes do not directly reveal which selection is optimal. Instead, they affect how the quantum state can interfere with later operations.
The cost layer is controlled by a parameter commonly written as "γ" (gamma). Its value determines the strength of the phase evolution associated with the cost function.
In a QAOA circuit, the cost layer is followed by a mixing layer. The two layers work together: the cost layer encodes information about the objective, while the mixing layer changes the amplitudes of the possible states.
Repeating these layers gives the algorithm more opportunities to shape the measurement distribution. However, increasing the number of layers also increases circuit complexity and may increase the effects of noise on real or noisy-simulated hardware.
The exact cost-layer operations depend on the mathematical encoding and its conversion into a quantum Hamiltonian. We will derive those operations from the validated formulation rather than assume that the original classical objective can be applied directly as a quantum gate.
4.3 The Mixing Layer
The mixing layer is the part of QAOA that helps the quantum state explore different candidate solutions.
After the cost layer applies phase changes based on the objective function, the mixing layer applies additional quantum operations that change the amplitudes of the possible states. These changes affect how the states interfere during later layers and ultimately influence the measurement probabilities.
A common choice for QAOA is the standard X-mixer, which applies rotations around the X axis of each qubit. The mixing operation is controlled by a parameter commonly written as "β" (beta).
The cost and mixing layers serve different purposes:
- Cost layer: Encodes information about the objective through phase changes.
- Mixing layer: Changes the quantum state to help shape the distribution of candidate solutions.
Together, these operations form one QAOA layer. Applying multiple cost-and-mixing pairs produces a deeper circuit.
There is an important limitation for constrained optimization problems. The standard X-mixer can move between feasible and infeasible selections. Therefore, even if the classical problem has a capacity constraint, the circuit may still produce overweight solutions.
In our project, we must handle this carefully. Our chosen encoding and objective must discourage invalid solutions correctly, and our evaluation must explicitly measure the frequency of feasible outcomes.
The exact mixer and circuit structure will be selected and documented when we implement QAOA. We will not assume that a standard mixer automatically enforces the knapsack capacity constraint.
4.4) QAOA Depth and Parameters
QAOA repeats its cost and mixing operations in alternating layers. The number of repetitions is called the QAOA depth and is represented by the integer "p".
For example:
- p = 1: One cost layer and one mixing layer.
- p = 2: Two cost layers and two mixing layers.
- p = 3: Three cost layers and three mixing layers.
Each layer pair introduces two parameters: "γ" (gamma) for the cost operation and "β" (beta) for the mixing operation.
Therefore, a QAOA circuit with depth "p" has "2p" parameters in the standard parameterization.
For example, at depth "p = 2", the parameter set contains two gamma values and two beta values.
Increasing "p" gives the circuit more parameters and additional opportunities to shape the measurement distribution. However, it also generally increases circuit size and can increase the effects of noise.
A larger depth does not automatically produce better results, especially on noisy hardware. The optimizer must find useful parameter values, and the compiled circuit must still be executable on the target processor.
In this project, we will investigate how QAOA depth affects solution quality and circuit metrics. We will compare the results using consistent experimental settings and report both the performance and the cost of deeper circuits.
The selected depth values and parameter-optimization procedure will be documented in the experimental configuration, rather than assumed in advance to be optimal.
4.5) The Classical Optimizer
QAOA is a hybrid quantum-classical algorithm because it combines quantum circuit execution with classical parameter optimization.
The quantum circuit uses the current parameter values to generate measurement outcomes. A classical computer then evaluates those outcomes and calculates a performance measure that the optimizer attempts to improve.
The optimizer updates the QAOA parameters, "γ" (gamma) and "β" (beta), and the circuit is evaluated again. This process repeats until a stopping condition is reached.
The optimization loop can be summarized as follows:
1. Choose initial QAOA parameter values.
2. Execute the parameterized quantum circuit.
3. Collect measurement counts.
4. Evaluate the measured solutions using the chosen objective.
5. Let the classical optimizer propose updated parameters.
6. Repeat until the stopping condition is satisfied.
The choice of objective matters. For example, an optimizer that maximizes the probability of measuring the exact optimum is solving a different optimization task from one that minimizes the expected QUBO energy.
The choice of optimizer, initial parameters, random seed, stopping condition, and number of circuit evaluations can all affect the results.
For a fair comparison between Processor A and Processor B, we must document these choices and apply a consistent procedure wherever possible. We must also clearly distinguish between parameters optimized using an ideal simulator and results obtained from noisy simulations.
A successful optimization run does not guarantee that QAOA has found the global best parameters. We will therefore report the experimental procedure and evaluate the resulting measurement distributions against the exact classical reference solution.
4.6) Evaluating QAOA Results
QAOA produces a distribution of measurement outcomes rather than guaranteeing the optimal solution on every execution. We therefore need quantitative metrics to evaluate its performance.
For our knapsack problem, we will use the following metrics.
1. Optimal-solution probability
This measures how frequently the circuit produces the exact classical optimal selection: items A, B, C, and D, with total value 26 and total weight 14.
It is calculated as the number of shots that produce the optimal selection divided by the total number of shots.
2. Feasible-solution probability
This measures the fraction of measurement outcomes whose selected items satisfy the capacity constraint.
It is calculated as the number of feasible shots divided by the total number of shots.
3. Approximation ratio
This compares the value of a solution with the value of the classical optimum. For a feasible solution with total value "V", the ratio is:
$$
\text{Approximation Ratio} = \frac{V}{26}
$$
For example, a feasible solution with value 25 has an approximation ratio of:
$$
\frac{25}{26} \approx 0.962
$$
This means its value is approximately 96.2% of the optimal value. For a fair aggregate comparison, we must specify whether the ratio is calculated for the best measured feasible solution or averaged over shots.
4. Circuit depth and gate count
These metrics describe the compiled circuit's implementation cost. We will report circuit depth, total gate count, CX gate count, and SWAP count where applicable.
5. Reproducibility
We will record the relevant random seeds, shot count, noise settings, transpiler configuration, optimizer settings, and software versions so that the experiments can be repeated and checked.
No single metric tells the whole story. A processor may have a lower circuit depth but a lower optimal-solution probability, or it may produce many feasible solutions without frequently finding the optimum.
Our comparison will therefore consider solution quality, feasibility, circuit cost, noise, and reproducibility together.
4.7)The Complete QAOA Workflow
The QAOA workflow combines mathematical modeling, quantum circuit execution, and classical optimization. Each stage has a specific purpose, and errors in an earlier stage can affect every result that follows.
Our workflow consists of the following steps:
1. Define the problem: Specify the five items, their values and weights, and the capacity of 15.
2. Establish the classical optimum: Evaluate all 32 item selections to identify the best feasible solution, with value 26 and weight 14.
3. Construct the mathematical encoding: Convert the constrained knapsack problem into a suitable objective and verify that it preserves the intended optimum.
4. Build the QAOA circuit: Prepare the initial state and apply the parameterized cost and mixing operations.
5. Optimize the parameters: Use a classical optimizer to search for useful QAOA parameter values.
6. Compile for each processor: Map the logical circuit onto the specified hardware connectivity and supported gates.
7. Run ideal and noisy simulations: Evaluate the circuit without noise and with the specified noise model.
8. Analyze the measurements: Calculate optimal-solution probability, feasible-solution probability, approximation ratio, and circuit metrics.
9. Compare the processors: Investigate how connectivity, compilation overhead, and noise influence the results.
10. Verify reproducibility: Record the configurations, random seeds, software versions, and procedures needed to reproduce the experiments.
The order of these steps matters. For example, a quantum circuit cannot provide meaningful evidence about the original knapsack problem if its mathematical encoding is incorrect.
Likewise, a difference between Processor A and Processor B should not automatically be attributed to connectivity unless other relevant experimental choices are controlled or their effects are explained.
Our aim is to produce a transparent, reproducible comparison supported by validated mathematics and measured results, rather than relying on claims of quantum advantage without sufficient evidence.
5) Processor Architectures and Experimental Configuration
The performance of a quantum algorithm depends not only on its mathematical formulation but also on how its circuit is implemented on the target processor.
Quantum processors differ in their number of physical qubits, connectivity, supported gate operations, and error characteristics. These differences can affect circuit compilation, gate count, circuit depth, and the quality of measured solutions.
For PS-O3, we will investigate two specified processor configurations: Processor A and Processor B. Both will be evaluated using the same knapsack problem and the same specified synthetic noise rates.
Our goal is to understand how their hardware connectivity influences the implementation and performance of QAOA. We will use the official processor specifications provided for the challenge and will not change the specified qubit counts.
5.1 )Processor Specifications and Connectivity
A processor's connectivity describes which pairs of physical qubits can directly interact through two-qubit gates. We represent each connection as a pair of qubit indices.
The official PS-O3 configurations are:
Specification| Processor A| Processor B
Physical qubits| 5| 9
Number of listed connections| 4| 12
Supported basis gates| "rz", "sx", "x", "cx"| "rz", "sx", "x", "cx"
Processor A connections:
"(0,1), (1,2), (1,3), (3,4)"
Processor B connections:
"(0,1), (1,2), (1,6), (2,3), (2,6), (2,5), (3,4), (4,5), (5,6), (6,7), (6,8), (8,0)"
These connection lists define the hardware graphs used in our experiments. Each number identifies a physical qubit, and each pair represents a specified connection.
Processor A has five physical qubits and four listed connections. Processor B has nine physical qubits and twelve listed connections. However, the number of connections alone does not determine which processor performs better.
The effect of connectivity depends on how the logical circuit is mapped to physical qubits, which interactions the circuit requires, and how the compiler handles interactions that are not directly supported.
5.2) Supported Basis Gates
A quantum processor configuration specifies the gate operations that the compiler can use to express a circuit. This supported set is commonly called the basis gate set.
For both Processor A and Processor B, the specified basis gates are:
"rz", "sx", "x", and "cx"
These gates have different roles:
- RZ: Rotates a qubit's state around the Z axis of the Bloch sphere.
- SX: Performs a square-root-of-X operation.
- X: Implements a bit flip on a qubit's computational basis state.
- CX: A two-qubit controlled-X gate that flips its target qubit when its control qubit is 1.
A circuit written using other gates may need to be decomposed into operations supported by the target configuration. The transpiler performs this and other compilation tasks, including mapping logical qubits to physical qubits and adapting the circuit to the available connectivity.
Compilation can introduce additional operations. For example, when a required two-qubit interaction cannot be implemented directly on the mapped physical qubits, the compiler may use SWAP gates or other routing strategies to move quantum information.
For our comparison, we will compile both processor configurations using the specified basis gates and the same transpiler optimization level. We will then measure the resulting circuit depth, total gate count, CX count, and SWAP overhead.
These metrics will help us determine whether the different connectivity structures lead to different implementation costs for the same logical algorithm.
We will preserve these configurations throughout the comparison and report the actual compiled circuit metrics for each processor.
5.3 )Noise Model and Simulation Settings
Quantum noise can affect the measured results of a circuit. To compare Processor A and Processor B fairly, the PS-O3 experiments specify the same synthetic noise rates for both configurations.
The specified noise parameters are:
Parameter| Value| Meaning
Single-qubit depolarizing error| "0.001" (0.1%)| Noise rate for single-qubit gates
Two-qubit CX depolarizing error| "0.005" (0.5%)| Noise rate for CX gates
Readout error| "0.01" (1%)| Probability of an incorrect recorded measurement outcome
Transpiler optimization level| "1"| Compilation optimization setting
Random seed| "42"| Seed specified for reproducible experimental configuration
Number of shots| "4096"| Number of circuit executions per measurement experiment, unless otherwise specified
These settings provide a common baseline for comparing the two processor configurations.
Single-qubit depolarizing error: represents noise associated with single-qubit operations under the selected noise model.
Two-qubit depolarizing error: represents noise associated with CX operations. Its specified rate is higher than the single-qubit rate.
Readout error: models the possibility that the recorded measurement bit differs from the intended measurement outcome.
Transpiler optimization level: controls the compiler's optimization strategy. We will keep it at the specified level so that compilation settings are consistent across the comparison.
Random seed: helps make supported randomized operations reproducible. A seed alone does not guarantee identical results across different software versions or execution environments.
Shots: each shot is one execution of the circuit followed by measurement. With 4,096 shots, the measured counts approximate the circuit's output probability distribution.
We must implement these settings in the actual experiment configuration and verify that readout error is not accidentally set to zero. Merely documenting the correct rates in this README is not sufficient.
We will distinguish ideal simulations, which exclude the specified noise model, from noisy simulations, which apply it. Results from these two conditions will be reported separately.
5.4) Transpilation and Qubit Mapping
A quantum algorithm is initially described as a logical circuit. This circuit specifies the qubits and operations required by the algorithm without necessarily accounting for a particular processor's physical layout.
Before execution, the circuit must be compiled for the target processor. In Qiskit, this process is called transpilation.
Transpilation can perform several tasks:
- Decompose gates into the supported basis gates.
- Map logical qubits to physical qubits.
- Route two-qubit operations to respect the processor's connectivity.
- Optimize the circuit to reduce implementation costs.
Logical qubits are the qubits used to describe the algorithm. Physical qubits are the qubits available in the specified processor configuration.
A logical circuit may require an interaction between two qubits that are not directly connected in the hardware graph. The transpiler must then find a way to implement the interaction using the available connections.
One possible approach is to insert SWAP gates. A SWAP gate exchanges the quantum states of two connected qubits, allowing the compiler to change where logical quantum information is located in the physical layout.
However, SWAP gates are not free. They require additional operations and can increase gate count, circuit depth, and exposure to noise.
The transpiler may use different routing and optimization strategies, so the number of inserted SWAP gates depends on the circuit, the initial layout, the connectivity, and the compilation procedure.
In our experiments, we will use the specified transpiler optimization level of 1 and record the resulting circuit metrics for both processors. We will also document the mapping and compilation settings needed to reproduce the comparison.
A fair analysis must distinguish between the circuit's original logical requirements and the extra implementation cost introduced by compiling it for a particular processor.
5.5) Fair Processor Comparison
A fair comparison requires us to distinguish between the effects of processor connectivity and the effects of the mathematical encoding.
The two processor configurations differ in their available qubits and connectivity:
- Processor A: 5 qubits and 4 listed connections.
- Processor B: 9 qubits and 12 listed connections.
We will evaluate the following factors:
1. Problem correctness: Does the method identify valid knapsack selections and recover the known classical optimum?
2. Circuit depth: How many sequential layers of operations are required after transpilation?
3. Gate count: How many operations are needed, particularly two-qubit gates?
4. SWAP overhead: How many additional SWAP gates are introduced to satisfy connectivity constraints?
5. Noise sensitivity: How do the specified gate and readout errors affect the measured outcomes?
6. Reproducibility: Can the experiment be repeated using the documented configuration and random seed?
The comparison must use the official processor connectivity, supported basis gates, noise rates, transpiler optimization level, and shot count specified for the challenge.
However, using identical settings does not automatically guarantee a fair comparison. Our current slack-variable encoding contains five item variables and four slack variables, requiring nine qubits. It therefore cannot be executed directly on Processor A's five-qubit configuration.
Before running the final benchmark, we must establish a mathematically valid approach for each processor and document any differences in encoding or circuit construction. We must not claim that connectivity alone explains a performance difference if the methods also differ in other important ways.
All reported metrics will be based on actual experiment outputs, not estimated or invented results.
6) Experimental Methodology
This section describes how the knapsack formulation and QAOA experiments will be tested, measured, and compared.
The experimental process will separate mathematical correctness, ideal quantum-circuit behaviour, and noisy simulation results. This separation is important because a mathematically correct model can still produce poor measured results when the circuit is deep or noise affects its execution.
6.1 Experimental Objectives
The experiments will address five main questions:
1. Correctness: Does the mathematical formulation represent the original 0/1 knapsack problem correctly, and does it preserve the known optimal solution?
2. Solution quality: How often does QAOA produce the optimal selection, and how often does it produce a feasible selection?
3. Circuit efficiency: How do circuit depth, gate count, two-qubit gate count, and SWAP overhead differ between the processor configurations?
4. Noise sensitivity: How do the specified depolarizing and readout errors affect solution quality?
5. Reproducibility: Can the experiments be repeated using the documented settings, random seed, and number of measurement shots?
These objectives correspond to the challenge's emphasis on correctness, processor benchmarking, circuit analysis, reproducibility, and explanation.
No experimental result will be reported as measured until the corresponding experiment has actually been executed and checked.
6.2) Mathematical Validation Before Quantum Execution
Before running QAOA, we will verify the mathematical formulation using classical computation.
The validation will include the following checks:
1. Exhaustive item enumeration: Evaluate all (2^5 = 32) possible selections of the five items.
2. Feasibility checking: Calculate each selection's total weight and verify that it does not exceed the capacity of 15.
3. Objective checking: Calculate the total value of every selection and identify the maximum value among feasible selections.
4. Reference-solution verification: Confirm that selecting A, B, C, and D gives total weight 14 and total value 26.
5. Encoding verification: Check that the mathematical objective and constraint penalty assign the intended costs to feasible and infeasible selections.
6. Independent cross-check: Compare the encoded model's preferred solutions with the original knapsack problem's solutions.
For the slack-variable formulation, we must additionally verify all (2^9 = 512) assignments of the five item variables and four slack variables. Each assignment must be checked against the original problem, not merely against the encoded objective.
These checks will be implemented and executed before the quantum experiments. Until then, they are planned validation steps rather than completed test results.
Important: Passing the mathematical checks does not prove that QAOA will find the optimum reliably. It establishes that the model being tested represents the intended optimization problem.
6.3) Experimental Stages
The experiments will be organized into four stages.
Stage 1 — Classical baseline
Solve the original knapsack problem by enumerating all 32 item selections. Record the optimal value, total weight, and item selection. This provides an independent reference for evaluating QAOA.
Stage 2 — Ideal simulation
Run the QAOA circuit without an added noise model. Examine the measured distribution and determine whether the algorithm produces the optimal selection and other feasible solutions.
Stage 3 — Noisy simulation
Apply the official synthetic noise settings to investigate how depolarizing errors and readout errors affect the measured outcomes. Keep the specified shot count and other configuration settings consistent with the challenge requirements.
Stage 4 — Processor comparison
Compare the results and transpiled circuit metrics for Processor A and Processor B. Record solution quality, circuit depth, gate counts, two-qubit operations, and SWAP overhead.
Before the final comparison, we must verify that the chosen formulation and circuit construction are valid for each processor's available qubits and connectivity. If different encodings are necessary, those differences will be documented so that the comparison remains scientifically meaningful.
Each stage will be run and checked before its results are included in the final report.
6.4) Evaluation Metrics
The following metrics will be used to evaluate the experiments.
1. Optimal-solution probability
The fraction of measured outcomes that correspond to the known optimal item selection, A + B + C + D, with total value 26 and total weight 14.
Optimal-solution probability measures how often the algorithm produces the best known answer.
2. Feasible-solution probability
The fraction of measured outcomes whose selected items have total weight no greater than 15.
A feasible result satisfies the original capacity constraint, regardless of whether it achieves the maximum value.
3. Approximation ratio
For a feasible measured solution, its approximation ratio is its value divided by the optimal value of 26.
For example, a feasible solution with value 25 has an approximation ratio of:
$$
\frac{25}{26} \approx 0.9615
$$
This means its value is approximately 96.15% of the optimal value.
For an overall experiment summary, we will report the average value of feasible outcomes separately from the feasible-solution probability, rather than treating infeasible outcomes as valid knapsack solutions.
4. Circuit depth
The number of sequential circuit layers after transpilation. Lower depth can reduce exposure to noise, although depth alone does not determine circuit quality.
5. Gate counts
The total number of gates and the number of two-qubit gates, particularly CX gates, after transpilation.
6. SWAP overhead
The number of SWAP gates introduced during routing, reported separately when possible. This helps show how processor connectivity affects circuit implementation.
7. Reproducibility
The experiment configuration, random seeds, shot count, and recorded results will be documented so that the experiments can be repeated.
All probability estimates will be calculated from actual measurement counts. Circuit metrics will be taken from the transpiled circuits, not estimated from the logical circuit.
6.5) Experimental Controls
An experimental control is a setting that is kept consistent so that differences in the results can be interpreted more reliably.
The following settings will be documented and controlled wherever the experiment permits:
Setting| Official configuration
Knapsack capacity| 15
Item values| "[10, 4, 7, 5, 8]"
Item weights| "[5, 3, 4, 2, 6]"
One-qubit depolarizing error| 0.001
Two-qubit CX depolarizing error| 0.005
Readout error| 0.01
Transpiler optimization level| 1
Random seed| 42
Measurement shots| 4096
The processor-specific qubit counts and connectivity will follow the official specifications documented in Section 5.1.
The ideal and noisy simulations will be reported separately. The ideal simulation will not include the synthetic noise model, while the noisy simulation will use the specified error settings.
The QAOA depth, parameter initialization, classical optimizer, and stopping criteria must also be recorded. If any of these settings differ between experiments, the difference will be documented.
Important limitation: Identical noise rates and shot counts do not, by themselves, guarantee a perfectly controlled comparison. The encodings, logical circuits, transpilation results, and optimization procedures must also be examined. In particular, the nine-variable slack formulation cannot fit directly on Processor A's five qubits.
These controls will be verified against the implementation before results are reported.
6.6) Reproducibility and Experiment Records
Reproducibility means that another person can follow the documented procedure and obtain results that can be compared with ours.
For every experiment, we will record:
- Processor configuration: The selected processor, available qubits, connectivity, and supported basis gates.
- Problem formulation: The encoding, penalty coefficient, and any additional variables or constraints.
- QAOA configuration: The circuit depth parameter (p), initial parameter values, classical optimizer, and stopping criteria.
- Simulation configuration: The ideal or noisy simulation mode, noise parameters, transpiler optimization level, random seeds, and shot count.
- Circuit statistics: Transpiled depth, total gate count, two-qubit gate count, and SWAP count.
- Measurement results: Raw counts, optimal-solution probability, feasible-solution probability, and solution-value statistics.
Random seeds will be recorded wherever the relevant software components support seeded randomness. A seed improves repeatability but does not guarantee identical results across every software version or execution environment.
The project will document the software environment and package versions used for the final experiments. Where possible, raw measurement counts and machine-readable result files will be retained alongside summary tables.
Results will be labelled as ideal, noisy, simulated, or hardware-executed as appropriate. Simulated results will not be presented as results obtained from a physical quantum processor.
Only results that have actually been generated and checked will be included as experimental findings.
6.7 )Results Analysis and Interpretation
The results will be analyzed by separating solution quality from circuit efficiency.
First, the measured outcomes will be checked against the original knapsack problem. This will establish whether the algorithm produces feasible selections and how frequently it identifies the optimal solution.
Next, the transpiled circuits will be compared to investigate how connectivity affects implementation. We will examine circuit depth, gate counts, two-qubit operations, and SWAP overhead.
Finally, ideal and noisy results will be compared to investigate how the specified noise model changes the measurement distribution and solution quality.
The analysis will distinguish between observations and explanations. For example, if Processor B produces a shallower circuit, we will report that measurement and investigate whether its connectivity explains the difference. We will not automatically conclude that more qubits or more connections guarantee better performance.
Any unexpected results, limitations, and differences between the two implementations will be discussed explicitly.
The final conclusions will be based on measured data, mathematical validation, and reproducible experiments rather than assumptions about which processor should perform better.
