# ant-colony-optimization

[Processing](https://processing.org/) project for
* (i) [Ant Colony Optimization](#aco) (ACO) simulation ([examples](#all-examples))

## Dependencies

All dependencies of this project are native to Processing platform.

## Contact / License

Feel free to contact me by mail: guilherme.farto@gmail.com

---

<a name="aco"></a>
## Ant Colony Optimization (AntColonyOptimization.pde)
> Based on Ant Colony Optimization algorithm - a probabilistic technique for solving computational problems which can be reduced to finding good paths through graphs

Usage:

`Open the main .pde file (AntColonyOptimization.pde) and run it by the Processing IDE`
* Pressing <kbd>CTRL</kbd>+<kbd>R</kbd>; or
* Selecting menu <kbd>Sketch</kbd> and <kbd>Run</kbd>;

### Main concepts of Ant Colony Optimization (introduction and concepts)

asdf

### Classes of Ant Colony Optimization

* **Ant.pde**

> Class that represents the ant entity.

Each ant is uniquely identified through the attribute called `id`.
  
The attributes of an object of the Ant class are:
  
```python
    int id

    int scale
    int x, y # (ant position at map)

    boolean hasFood
    float foodLoaded
    int bored
    float pheromoneForceForFood
    float pheromoneForceForAnthill
```

The methods of an object of Ant class are:

```java
    void draw() { ... }
    void drawSmallFood() { ... }

    void step() { ... }
    void depositFood() { ... }
    boolean bite(Food food) { ... }
    void releasePheromone(float pheromoneForce, Map map) { ... }
```

Ants can be added to the ACO simulation in two ways:

* By clicking the left mouse button;
* By starting a simulation on a map that contains only the anthill and food (thus, 50 ants will be dynamically added to the simulation);

> This amount of ants can be modified by changing the constant value of the AntColonyOptimization class based on the following `snippet`:

```java
	final int DEFAULT_ANTS_COUNT = 50
```

Each ant will perform two essential activities during the simulation:

* Search for food along the map;
* Transporting and depositing food in the anthill;

Ants will release pheromone in the path traveled regardless of the activity they are performing. Over time, the pheromone attraction force will be reduced. The pulling force of an ant's pheromone will be reset to the default value (i) when the ant finds the food and (ii) when the ant returns and deposits the food in the anthill (and go out in search of food again).

The release of pheromones by an ant contributes to the orientation (or suggestion) the other in a way that can guide you in search of food, as well as in nature. A longer time is needed for the trail pheromone to evaporate when more ants go through the predetermined path. If a trail pheromone is no longer used or is underutilized for a given period, there will be evaporation of pheromone. As a result, the pheromone trail will be reduced and / or erased, restricting the possibility of other ants moving in the same direction.

The pheromone release and evaporation processes contribute, respectively, (i) to strengthen and increase the probability of other ants follow the same path in search of food and (ii) to avoid convergence to an optimal local solution, allowing bad decisions (paths) to be forgotten.

The ACO simulation assumes that ants can become bored and thus stop moving for a brief period.

* **Anthill.pde**

  > asdf

  asdf

* **Food.pde**

  > asdf

  asdf

* **Pheromone.pde**

  > asdf

  asdf

* **Map.pde**

  > asdf

  asdf

* **AntColonyOptimization.pde**

  > asdf

  asdf

<a name="aco-instructions"></a>
## Instructions for ACO simulation (keyboard and mouse commands)

asdf

| Type          | Command            | Description                               |
| ------------- | ------------------ | ----------------------------------------- |
| `Keyboard`    | Press <kbd>S</kbd> | Start or stop simulation                  |
| `Keyboard`    | Press <kbd>=</kbd> | Increase food size                        |
| `Keyboard`    | Press <kbd>-</kbd> | Decrease food size                        |
| `Keyboard`    | Press <kbd>0</kbd> | Change framerate to 2                     |
| `Keyboard`    | Press <kbd>1</kbd> | Change framerate to 10                    |
| `Keyboard`    | Press <kbd>3</kbd> | Change framerate to 30                    |
| `Keyboard`    | Press <kbd>6</kbd> | Change framerate to 60                    |
| `Keyboard`    | Press <kbd>F</kbd> | Show or hide pheromone for food           |
| `Keyboard`    | Press <kbd>C</kbd> | Show or hide pheromone for colony         |
| `Mouse`       | `Left` click       | Create an ant at `(x, y)` mouse event     |
| `Mouse`       | `Right` click      | Create a food at `(x, y)` mouse event     |
| `Mouse`       | `Center` click     | Create an anthill at `(x, y)` mouse event |

<a name="all-examples"></a>
## Examples

<a name="aco-examples-1"></a>
### > Setting anthill, ants (in total of 10), and food repositories

asdf

| aco-simulation_1.png     | aco-simulation_2.png     | aco-simulation_3.png     |
| ------------------------ | ------------------------ | ------------------------ |
| ![](examples/1/aco-simulation_1.png) | ![](examples/1/aco-simulation_2.png) | ![](examples/1/aco-simulation_3.png) |

| aco-simulation_4.png     | aco-simulation_5.png     |
| ------------------------ | ------------------------ |
| ![](examples/1/aco-simulation_4.png) | ![](examples/1/aco-simulation_5.png) |

asdf

<a name="aco-examples-2"></a>
### > Setting anthill and food repositories but generating 50 random ants

asdf

| aco-simulation_1.png     | aco-simulation_2.png     | aco-simulation_3.png     | aco-simulation_4.png     |
| ------------------------ | ------------------------ | ------------------------ | ------------------------ |
| ![](examples/2/aco-simulation_1.png) | ![](examples/2/aco-simulation_2.png) | ![](examples/2/aco-simulation_3.png) | ![](examples/2/aco-simulation_4.png) |

| aco-simulation_5.png     | aco-simulation_6.png     | aco-simulation_7.png     | aco-simulation_8.png     |
| ------------------------ | ------------------------ | ------------------------ | ------------------------ |
| ![](examples/2/aco-simulation_5.png) | ![](examples/2/aco-simulation_6.png) | ![](examples/2/aco-simulation_7.png) | ![](examples/2/aco-simulation_8.png) |

| aco-simulation_9.png     | aco-simulation_10.png    | aco-simulation_11.png    |
| ------------------------ | ------------------------ | ------------------------ |
| ![](examples/2/aco-simulation_9.png) | ![](examples/2/aco-simulation_10.png) | ![](examples/2/aco-simulation_11.png) |

asdf

<a name="aco-future-directions"></a>
## Future directions

<a name="aco-future-directions-1"></a>
### > Multiple ant colonies for ACO

asdf

<a name="aco-future-directions-2"></a>
### > Setting obstacles and/or ant predators

asdf

<a name="aco-future-directions-3"></a>
### > Natural selection, genetic algorithms, and lifetime characteristics

asdf
