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
  
The attributes for Ant class are:
  
```java
	int id
	
	int scale
	int x, y // (ant position at map)
	
	boolean hasFood
	float foodLoaded
	int bored
	float pheromoneForceForFood
	float pheromoneForceForAnthill
```

The methods for Ant class are:

```java
    void draw() { ... }
    void drawSmallFood() { ... }

    void step() { ... }
    void depositFood() { ... }
    boolean bite(Food food) { ... }
    void releasePheromone(float pheromoneForce, Map map) { ... }
```

Ants can be added to the ACO simulation in two ways:

* By left-clicking the mouse button;
* By starting a simulation on a map that contains only the anthill and food (thus, 50 ants will be dynamically added to the simulation);

> This amount of ants can be modified by changing the constant value of the AntColonyOptimization class based on the following `snippet`:

```java
	final int DEFAULT_ANTS_COUNT = 50
```

Each ant will perform two essential activities during the simulation:

* Search for food along the map;
* Transport and deposit food in the anthill;

Ants will release pheromone in the trail traveled regardless of the activity they are performing. Over time, the pheromone attraction force will be reduced. The attraction force of an ant's pheromone will be reset to the default value (i) when the ant finds the food and (ii) when the ant returns and deposits the food in the anthill (and go out in search of food again).

The pheromones released by an ant contributes to the orientation (or suggestion) in a way that can guide other ants in the search of food, as well as in nature. A longer time is needed for the trail pheromone to evaporate when more ants go through the predetermined path. There will be evaporation of pheromone if a trail pheromone is no longer used or is underutilized for a given period. As a result, the pheromone trail will be reduced and/or erased, restricting the possibility of other ants moving in the same direction.

The release of pheromone release and evaporation processes support, respectively, (i) to strengthen and increase the probability of other ants follow trails in the search of food and (ii) to avoid convergence to an optimal local solution, allowing bad decisions (paths) to be forgotten.

The ACO simulation assumes that ants can become bored and thus stop moving for a brief period of time.

* **Anthill.pde**

> Class that represents the anthill entity.

There must be only one object of the Anthill class in an ACO simulation.

All the food collected by the ants will be deposited in the anthill (as long as the ants can return to the anthill through the trail pheromone).

The attributes for Anthill class are:

```java
	int scale
	int x, y // (anthill position at map)

	int totalOfFood
```

The methods for Anthill class are:

```java
	void draw() { ... }
	void depositFood(int foodLoaded) { ... }
```

An anthill can be added or redefined to the ACO simulation by middle-clicking the mouse button (scrollbar wheel button). A new one will be added if there is no anthill on the map. If it already exists, the current anthill will no longer exist and a new one will be created based on the position `(x, y)` of the last mouse click event.

* **Food.pde**

> Class that represents the food entity.

Each food is uniquely identified through the attribute called `id`.

The attributes for Food class are:

```java
	int id

	int scale
	int x, y // (food position at map)

	int value
```

The methods for Food class are:

```java
	void draw() { ... }

	void updateValue() { ... }
	boolean hasValue() { ... }
```

Food can be added to the ACO simulation by right-clicking the mouse button.

The size of the food can be modified by pressing <kbd>=</kbd> (to increase food size) or <kbd>-</kbd> (to decrease food size).

Each (block of) food will contain a random value ranging from 4 to 10. In this way, the ACO simulation can exercise the algorithm considering that food is available in varying quantities (larger ones and smaller ones) - just as in the real world.

This value range can be modified in the constructor method of the Food class based on the following `snippet`:

```java
	this.value = (int) random(4, 10);
```

Food will cease to exist when its value is equal to or less than zero (0). This means that one or more ants have already withdrawn (or bitten) the food completely.

* **Pheromone.pde**

> Class that represents the pheromone entity (pheromone secreted or excreted by ants).

Each pheromone is uniquely identified through the attribute called `id`.

The attributes for Pheromone class are:

```java
	String id // concat of x + ";" + y

	int scale
	int x, y // (pheromone position at map)

	float value
```

The methods for Pheromone class are:

```java
	void draw() { ... }

	boolean update(float pheromoneForce) { ... }
	boolean evaporate(float evaporationRate) { ... }
	static String getPheromoneId(int x, int y) { ... }
```

Pheromones are instantiated and added to the ACO simulation in two ways:

* When the ants leave the anthill and search for food;
* When the ants find food and return to the anthill (to deposit the food collected);

Therefore, the ACO simulation will have two trails of pheromones that are reinforced when ants transit the same path, but also evaporate when they cease to transit through it.

It is important to mention that the strength (or efficiency) of an ant's pheromone is reduced over time. However, when food is found or the anthill is located, its pheromone attraction force will be reseted to the default value.

* **Map.pde**

> Class that represents the map (or terrain) entity in which ants, food, pheromones, and anthill are contained.

By default, the ACO simulation uses two Map objects: (i) a map that contains the food trail pheromones and (ii) a map that contains the anthill trail pheromones.

The attributes for Map class are:

```java
	final float DEFAULT_PHEROMONE = 100
	final float EVAPORATION_RATE = .999
	final float USE_RATE = .995

	int scale
	int width
	int height

	HashMap<Integer, Ant> ants
	HashMap<Integer, Food> foods
	Anthill anthill

	HashMap<String, Pheromone> pheromones = new HashMap<String, Pheromone>()
	ArrayList<Pheromone> pheromonesToRemove = new ArrayList<Pheromone>()
	
	boolean showPheromone = true
```

The methods for Map class are:

```java
	void draw() { ... }
	void drawFieldLimits() { ... }
	void drawFieldInnerLimits() { ... }
	void drawPheromones() { ... }

	void clear() { ... }

	void setAnthill(Anthill anthill) { ... }
	Anthill getAnthill() { ... }
	Anthill getAnthill(int x, int y, boolean isNear) { ... }

	void start() { ... }
	void step() { ... }

	int[] getStrongestPath(Ant ant) { ... }

	void releasePheromone(int x, int y, float pheromoneForce) { ... }
	void createPheromone(int x, int y, float pheromoneForce) { ... }

	float getPheromone(Ant ant, int[] directions) { ... }
	float getPheromone(int[] directions) { ... }
	float getPheromone(int x, int y) { ... }

	void evaporatePheromones() { ... }

	Food getFood(int x, int y, boolean isNear) { ... }
	void updateFood(Food food) { ... }

	int[] getDirectionsForObject(int x, int y, int[] directions) { ... }
	Object hasObjectAt(int x, int y) { ... }

	void showHidePheromone() { ... }

	int getTotalOfFood() { ... }
```

The Map class is responsible for the interaction between entities that represent ants, anthill, and food. It is also through the Map that occurs the release and evaporation of pheromone trails. In this way, it provides the necessary mechanism for the orientation of ants by the pheromone approach.

* **AntColonyOptimization.pde**

> Main class that represents the integration of all entities (ant, anthill, food, pheromone, and map) of the Ant Colony Optimization context.

The AntColonyOptimization class is responsible for setting and simulating experiments based on the ACO approach.

The main attributes for AntColonyOptimization class are:

```java
	final int DEFAULT_ANTS_COUNT = 50
	final int DEFAULT_SCALE = 6
	final int COLONY_SIZE = 600
	final int PANEL_OFFSET = COLONY_SIZE
	final int PANEL_SIZE = 200
	
	HashMap<Integer, Ant> ants = new HashMap<Integer, Ant>()
	HashMap<Integer, Food> foods = new HashMap<Integer, Food>()
	Anthill anthill
	
	Map mapFood = new Map(DEFAULT_SCALE, COLONY_SIZE, COLONY_SIZE, ants, foods)
	Map mapColony = new Map(DEFAULT_SCALE, COLONY_SIZE, COLONY_SIZE, ants, foods)
	
	int foodSize = 5
	
	boolean started = false
```

The methods for AntColonyOptimization class are:

```java
	void setup() { ... }

	void draw() { ... }
	void drawField() { ... }
	void loadFieldSize() { ... }

	void createAnt(int x, int y) { ... }
	void createFood(int x, int y) { ... }
	void createAnthill(int x, int y) { ... }
	void createRandomAnthill() { ... }

	void increaseFoodSize() { ... }
	void decreaseFoodSize() { ... }

	void mousePressed() { ... }
	void keyPressed() { ... }
```

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
| `Mouse`       | `Left`-click       | Create an ant at `(x, y)` mouse event     |
| `Mouse`       | `Right`-click      | Create a food at `(x, y)` mouse event     |
| `Mouse`       | `Center`-click     | Create an anthill at `(x, y)` mouse event |

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
