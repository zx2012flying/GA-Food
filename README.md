# GA-Food

Tailor-made GA algorithm for desinging chocolate chip cookie

This GA is based on the DEAP framework (see https://github.com/deap/deap).
The original algorithm was modified already so that it can be used easily for designing new chocolate chip cookie.
For the detailed info of the design case study, please refer to XX

## Installation

We encourage you to use pip to install GA-Food on your system.

```bash
pip install git+git://github.com/zx2012flying/Genetic-Algorithm.git
```

## Example
The following code gives a quick overview how simple it is to implement the Onemax problem optimization with genetic algorithm using DEAP. More examples are provided here.

```python
import random
from deap import creator, base, tools, algorithms

creator.create("FitnessMax", base.Fitness, weights=(1.0,))
creator.create("Individual", list, fitness=creator.FitnessMax)

toolbox = base.Toolbox()

toolbox.register("attr_bool", random.randint, 0, 1)
toolbox.register("individual", tools.initRepeat, creator.Individual, toolbox.attr_bool, n=100)
toolbox.register("population", tools.initRepeat, list, toolbox.individual)

def evalOneMax(individual):
    return sum(individual),

toolbox.register("evaluate", evalOneMax)
toolbox.register("mate", tools.cxTwoPoint)
toolbox.register("mutate", tools.mutFlipBit, indpb=0.05)
toolbox.register("select", tools.selTournament, tournsize=3)

population = toolbox.population(n=300)

NGEN=40
for gen in range(NGEN):
    offspring = algorithms.varAnd(population, toolbox, cxpb=0.5, mutpb=0.1)
    fits = toolbox.map(toolbox.evaluate, offspring)
    for fit, ind in zip(fits, offspring):
        ind.fitness.values = fit
    population = toolbox.select(offspring, k=len(population))
top10 = tools.selBest(population, k=10)
```
