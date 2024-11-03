# SWE_CAP2_Game_Automation

## **Brief Description of the Game and the Objectives**
In The Farmer Was Replaced, I play as a programmer in charge of automating a farm using a drone. My mission is to write code that instructs the drone to complete various farming tasks, from planting seeds to watering and harvesting crops. As I advance through levels, the challenges become more complex, requiring precise planning and optimization to manage the drone’s actions efficiently. The game combines coding skills with strategic problem-solving, pushing me to refine my automation process for maximum productivity and minimal resource use.

### Objectives

1. **Basic Crop Planting and Harvesting**: Guide the drone to plant and harvest crops on a grid according to basic instructions.

2. **Manage Crop-Specific Requirements**: Adhere to special planting rules for each crop, like spacing trees properly to avoid overcrowding.

3. **Optimize Harvesting Sequence**: Harvest crops in a specific order (e.g., largest to smallest for sunflowers) to maximize yield.

4. **Efficient Movement**: Minimize the drone’s travel time across the field with optimized paths and movement loops.

5. **Implement Polyculture**: Plant compatible crop types together to boost farm productivity.

6. **Watering and Fertilizing**: Add timely watering and fertilizing steps to ensure optimal crop growth.

7. **Resource Management**: Use resources like water and fertilizer effectively, reducing waste while ensuring crop health.

8. **Automation Refinement**: Continuously improve the automation process, allowing the drone to operate with minimal manual input. 

By working through these objectives, I learn to balance efficiency, resource management, and algorithmic problem-solving, all while managing the unique needs of a diverse set of crops.

# Table of Contents
- [Code Snippets and Explanation](#code-snippets-and-explanation)
- [Challenges and Learnings](#challenges-and-learnings)
- [References](#references)

# Code-Snippets-and-Explanation

## Step 1: Farming on 1 tile
### **Code:**

```python
harvest()
```
### **Explanation:**

The code runs and collects grass upto 5 and then the loops get unlocked

### **Demo:**

![Step_1](./Game1.mp4)

### **Code:**

```python
while True:
    if can_harvest():
        harvest()
    else:
        do_a_flip()
```
**Explanation:**

The code runs an infinite number of times and harvest the grass if the condition is true and else the drone does a flip and continue harvesting.

### **Code:**

```python
while True:
    if can_harvest():
        harvest()
        move(North)
```
### **Explanation:**

After expanding our tiles to `3 x 1` then while harvesting we can move north and harvest and continue the harvest.


### **Code:**

```python
while True:
	plant(Entities.Bush)
	if can_harvest():
		harvest()
		move(North)
	else:
		move(North)
```
### **Explanation:**

Uisng this code, we plant bush which is one of the entities and harvest both wood and grass alternately but at first one challenge that I faced was when I wrote this code: 

```python
 while True:
	plant(Entities.Bush)
	if can_harvest():
		harvest()
		move(North)
``` 
is that it waits for bush to be able to harvest so it was bit time consuming so I used else statement and moved the drone towards north if the wood is not harvestable it moves north harvesting grass and woods.



### **Note:**

Here in this step;
* I expand and the tiles got expanded to `1 x 3` from `1 x 1`.
* I unlocked speed of the drone so that I can harvest more.
* I upgraded the grass so that I can increase the yield of the grass.
* I unlocked senses so that that drone can see what's under it and where it is.
* I unlocked the operaters


## Step 2: Farming on `3 x 3` tile

### **Code:**

```python
clear()
move(South)
while True:
	for i in range(get_world_size()):
		move(North)
		if can_harvest():
			harvest()
			if num_items(Items.Hay) < 500:
				plant(Entities.Grass)
			else:
				plant(Entities.Bush)
	
	move(East)
```

### **Explanation:**

Now I have `3 x 3` farming tile so now I have also unlocked the loops so that it can run for infinite times setting the conditions. In this code I have set my drone to move 3 tiles to north and 3 tiles to east in my farming size which I called using `get_world_size()` function. What I did is that I will check if my hay is less than 500 or not and it is less than 500 then drone plants the entities grass and if it is greater than 500, it starts plantiing bushes for wood. I have used `clear()` and `move(South)` to clear all the states to starting position and after moving to 3 tiles north and return to south and again continue harvesting respectively.


### **Code:**
```python
clear()
move(South)
while True:
	for i in range(get_world_size()):
		move(North)
		if can_harvest():
			harvest()
			if num_items(Items.Hay) < 600:
				plant(Entities.Grass)
			elif num_items(Items.Wood) < 400:
				plant(Entities.Bush)
			else:
				if num_items(Items.Carrot_Seed) == 0:
					trade(Items.Carrot_Seed)
				if get_ground_type() == Grounds.Turf:
					till()
				plant(Entities.Carrots)
	
	move(East)
```

### **Explanation:**

When I execute this code, it checks the number of items I have by looking at the conditions I set and then it also checks if I have `Carrot_Seeds` and if I don't have the `Carrot_Seeds` then it trades using the `trade()` funtion. After trading the `Carrot_Seeds` before planning the `Carrots` it checks if the ground is tilled or not by using the `get_ground_type()` function and then only plants the carrots.

### **Code:**

```python
clear()
move(South)
while True:
	for i in range(get_world_size()):
		move(North)
		if can_harvest():
			#Harvest
			harvest()
			
			#Water Tank
			if num_items(Items.Water_Tank) < 100:
				trade(Items.Empty_Tank)
			#watering
			if get_water() < 0.75: #(b/w 0 - 1)
				use_item(Items.Water_Tank)
			#Hay
			if num_items(Items.Hay) < 600:
				if get_ground_type() == Grounds.Soil:
					till()
				plant(Entities.Grass)
			#Wood
			elif num_items(Items.Wood) < 400:
				if get_ground_type() == Grounds.Soil:
					till()
				plant(Entities.Bush)
			#Carrots
			else:
				if num_items(Items.Carrot_Seed) == 0:
					trade(Items.Carrot_Seed)
				if get_ground_type() == Grounds.Turf:
					till()
				plant(Entities.Carrots)
	
	move(East)
```

### **Explanation:**

In the watering part of the code, the character ensures it has enough filled water tanks and maintains an optimal water level for crops. First, it checks if the inventory contains fewer than 100 water tanks using `num_items(Items.Water_Tank) < 100`. If so, it calls `trade(Items.Empty_Tank)`, likely to acquire more water tanks or refill them. Then, the code checks the current water level with `if get_water() < 0.75`, and if the water level is below 75% (on a scale of 0 to 1), it uses one of the filled water tanks by calling `use_item(Items.Water_Tank)`. This keeps the crops adequately watered without wasting resources, as water tanks are only used when the level drops below the set threshold.

### **Code:**
```python
clear()
move(South)
#variables
num_watertank = 100
num_hay = 600
num_wood = 400
num_carrots = 100
#main loop
while True:
	for i in range(get_world_size()):
		move(North)
		if can_harvest():
			#Harvest
			harvest()
			
			#Water Tank
			if num_items(Items.Water_Tank) < num_watertank:
				trade(Items.Empty_Tank)
			#watering
			if get_water() < 0.75: #(b/w 0 - 1)
				use_item(Items.Water_Tank)
			#Hay
			if num_items(Items.Hay) < num_hay:
				if get_ground_type() == Grounds.Soil:
					till()
				plant(Entities.Grass)
			#Wood
			elif num_items(Items.Wood) < num_wood:
				if get_ground_type() == Grounds.Soil:
					till()
				plant(Entities.Bush)
			#Carrots
			elif num_items(Items.Carrot) < num_carrots:
				if num_items(Items.Carrot_Seed) == 0:
					trade(Items.Carrot_Seed)
				if get_ground_type() == Grounds.Turf:
					till()
				plant(Entities.Carrots)
	
	move(East)
```

### **Explanation:**

In this code I used the variables to give the values of the items i want to harvest
### **Note:**

In this step;
* The carrots are unlocked
* I unlocked the variables now that I can set the number of entities I want to keep as a condition.
* Unlocked the watering


## Step 4: Farming on `4 x 4` tile
 ### **Code:**
 ```python
clear()
move(South)
#variables
num_watertank = 100
num_hay = 2000
num_wood = 1000
num_carrots = 800
#main loop
while True:
	for i in range(get_world_size()):
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		if can_harvest():
			#Harvest
			harvest()
			
			#Water Tank
			if num_items(Items.Water_Tank) < num_watertank:
				trade(Items.Empty_Tank)
				
			#watering
			if get_water() < 0.75: #(b/w 0 - 1)
				use_item(Items.Water_Tank)
				
			#Hay
			if num_items(Items.Hay) < num_hay:
				if get_ground_type() == Grounds.Soil:
					till()
				plant(Entities.Grass)
				
			#Wood
			elif num_items(Items.Wood) < num_wood:
				if (x % 2 == 0 and y % 2 == 1) or (x % 2 == 1 and y % 2 == 0):
					plant(Entities.Tree)
				else:
					if get_ground_type() == Grounds.Soil:
						till()
					plant(Entities.Bush)
	
			#Carrots
			elif num_items(Items.Carrot) < num_carrots:
				if num_items(Items.Carrot_Seed) == 0:
					trade(Items.Carrot_Seed)
				if get_ground_type() == Grounds.Turf:
					till()
				plant(Entities.Carrots)
	
	move(East)
 ```

### **Explanation:**

In this code I wrote the code to plant trees so that we can increase the yield of the woods and here I needed to plant trees in checkerboard pattern so that trees can grow well. For that I used the `get_pos_x` and `get_pos_y` functions to get the positions where I can plant the trees where the positions are `odd` so that it's position remain in checkerboard pattern.


### **Code:**
**Main**
```python
clear()
move(South)
##variables
num_watertank = 100
num_hay = 7000
num_wood = 4000
num_carrots = 3000
##main loop
while True:
	for i in range(get_world_size()):
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		if can_harvest():
			
			##Harvest
			harvest()
			
			##Watering
			watering()
			
			##Planting
			planting()
			
				
	#Next Row
	move(East)
```

**Planting Function**
```python
def planting():
	#Hay
	if num_items(Items.Hay) < num_hay:
		if get_ground_type() == Grounds.Soil:
			till()
		plant(Entities.Grass)
				
	#Wood
	elif num_items(Items.Wood) < num_wood:
		if (x % 2 == 0 and y % 2 == 1) or (x % 2 == 1 and y % 2 == 0):
			plant(Entities.Tree)
		else:
			if get_ground_type() == Grounds.Soil:
				till()
			plant(Entities.Bush)
	
	#Carrots
	elif num_items(Items.Carrot) < num_carrots:
		if num_items(Items.Carrot_Seed) == 0:
			trade(Items.Carrot_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Carrots)
```

**Watering Function**
```python
def watering():
		#Water Tank
		if num_items(Items.Water_Tank) < num_watertank:
			trade(Items.Empty_Tank, 5)
		#watering
		if get_water() < 0.75: #(b/w 0 - 1)
			use_item(Items.Water_Tank)
```

### **Explanation:**

Unlocking the functions, I created a seperate windows for each function such as main, planting and the watering functions. After that, I called the functions of planting and watering in the main function. `Multi-trade` helped me trade more `Carrot_seeds` and `Empty_Tank` at a time and here I tarded for 5 using this line of codes `trade(Items.Empty_Tank, 5)` and `trade(Items.Carrot_Seed, 5)`.


### **Code:**
```python
clear()
do_a_flip()
move(South)
#variables
num_watertank = 100
num_hay = 10000
num_wood = 6000
num_carrots = 5000
num_pumpkins = 600
#main loop
while True:
	for i in range(get_world_size()):
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		if can_harvest():
			
			#Harvest
			harvest()
			
			#Watering
			watering()
			
			#Planting
			planting()
		else:
			if get_ground_type() == Grounds.Soil:
				till()
				
	#Next Row
	move(East)
```
**Planting Functions**
```python
def planting():
	#Sunflower
	if x == 0 and y == 0:
		if num_items(Items.Sunflower_Seed) == 0:
			trade(Items.Sunflower_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Sunflower)
		
	#Hay
	elif num_items(Items.Hay) < num_hay:
		if get_ground_type() == Grounds.Soil:
			till()
		plant(Entities.Grass)
				
	#Wood
	elif num_items(Items.Wood) < num_wood:
		if (x % 2 == 0 and y % 2 == 1) or (x % 2 == 1 and y % 2 == 0):
			plant(Entities.Tree)
		else:
			if get_ground_type() == Grounds.Soil:
				till()
			plant(Entities.Bush)
	
	#Carrots
	elif num_items(Items.Carrot) < num_carrots:
		if num_items(Items.Carrot_Seed) == 0:
			trade(Items.Carrot_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Carrots)
		
	
	#Pumpkins
	elif num_items(Items.Pumpkin) < num_pumpkins:
		if num_items(Items.Pumpkin_Seed) == 0:
			trade(Items.Pumpkin_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Pumpkin)
```
### **Explanation:**
I have unlocked a new function called `measure`, so whenever the `drone` is above a petal, we can measure the amount of petals because here I need to harvest the sunflower with the most petals to get more power which helps in harvesting faster.
#### Sunflower Planting:
- Sunflowers are set to be planted at a designated starting position `(x == 0 and y == 0)`, indicating that they may be grown in a fixed location, possibly as a decorative crop or one that has special requirements.

- The code checks if sunflower seeds are available (`num_items(Items.Sunflower_Seed) == 0`). If not, it trades for 5 more seeds.

- Then, if the ground is turf, it uses `till()` to prepare the soil, ensuring that the sunflower has an optimal growth environment.

- Finally, it plants the sunflower using `plant(Entities.Sunflower)`, maintaining the inventory and growth cycle for this specific crop.

### Pumpkin Planting:
- The pumpkin planting section checks if the inventory of harvested pumpkins is below the required amount (`num_items(Items.Pumpkin) < num_pumpkins`).

- If the pumpkin seed inventory is empty, it trades for more seeds to prevent any planting delays.

- Similar to sunflowers, it checks if the ground type is turf, tills the soil if necessary, and then plants the pumpkin using `plant(Entities.Pumpkin)`.

From this approach I can ensure that both sunflowers and pumpkins are planted only when conditions are ideal, keeping their production consistent with game objectives, which likely involve managing resources efficiently and meeting specific crop threshold I set.



### **Note:**

Functions that I unlocked in this step are;
* Tree
* Functions ( I can define new function using `def` keyword )
* I increased the yield of carrots to 300% and woods to 400% by upgrading the carrots and tree functions.
* multi-trade, so that I can buy seeds more at a time.


## Step 5: Farming on `5 x 5` tile

### **Code:**
```python
clear()
do_a_flip()
move(South)
#variables
num_watertank = 100
num_hay = 20000
num_wood = 16000
num_carrots = 1400
num_pumpkins = 10000
#main loop
while True:
	for i in range(get_world_size()):
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		if can_harvest():
			
			#Harvest
			harvest()
			
			#Watering
			watering()
			
			#Planting
			planting()
		else:
			if get_ground_type() == Grounds.Soil:
				till()
				
	#Next Row
	move(East)



def planting():
	#Sunflower
	if x == 0 and y == 0:
		if num_items(Items.Sunflower_Seed) == 0:
			trade(Items.Sunflower_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Sunflower)
		
	#Hay
	elif num_items(Items.Hay) < num_hay:
		if get_ground_type() == Grounds.Soil:
			till()
		plant(Entities.Grass)
				
	#Wood
	elif num_items(Items.Wood) < num_wood:
		if (x % 2 == 0 and y % 2 == 1) or (x % 2 == 1 and y % 2 == 0):
			plant(Entities.Tree)
		else:
			if get_ground_type() == Grounds.Soil:
				till()
			plant(Entities.Bush)
	
	#Carrots
	elif num_items(Items.Carrot) < num_carrots:
		if num_items(Items.Carrot_Seed) == 0:
			trade(Items.Carrot_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Carrots)
		
	
	#Pumpkins
	elif num_items(Items.Pumpkin) < num_pumpkins:
		if num_items(Items.Pumpkin_Seed) == 0:
			trade(Items.Pumpkin_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Pumpkin)


def watering():
		#Water Tank
		if num_items(Items.Water_Tank) < num_watertank:
			trade(Items.Empty_Tank, 5)
		#watering
		if get_water() < 0.75: #(b/w 0 - 1)
			use_item(Items.Water_Tank)
```

### **Note:**

In this step, where the farming tile is `5 x 5`, I just used the same code of the previous step by increasing the speed of the drone and yield of the entities so that I can unlock other important functions to farm. 


## Step 6: Farming on `6 x 6` tile

### **Code:**
```python
#main loop
while True:
	for i in range(get_world_size()):
		#buy stuff
		if num_items(Items.Sunflower_Seed) < 100:
			trade(Items.Sunflower_Seed, get_world_size())
		if num_items(Items.Carrot_Seed) < 100:
			trade(Items.Carrot_Seed, get_world_size())
		if num_items(Items.Pumpkin_Seed) < 100:
			trade(Items.Pumpkin_Seed, get_world_size())
			
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		if can_harvest():
			
			#Harvest
			harvest()
			
			#Watering
			watering()
			
			#Planting
			planting()
		else:
			if get_ground_type() == Grounds.Soil:
				till()
```

### **Explanation:**

In this part of my code, I added the new code to buy seeds to make sure I always have enough seeds for planting sunflowers, carrots, and pumpkins on the farm. I’ve set it up so that if I have fewer than 100 of any type of seed, the code will automatically trade for more. I use `get_world_size()` to decide how many seeds to buy, which means the amount I buy is based on the size of the area I’m managing. This way, I have enough seeds to cover the entire farm without going overboard and using up too much inventory space.

This keeps my farm’s planting process smooth and efficient, so I don’t have to worry about running out of seeds and interrupting the automation. It’s all about making sure my resources are in balance, letting me focus on optimizing other parts of my farm.

### **Note:**

- I maxed the upgrade level for `Grass`, `Trees` and `Carrots` which helped a lot in increasing the yield for hay, wood and carrots. 
- Now I expanded my farm size to `7 x 7` to harvest more sunflower for more power to speed up the drone.


## Step 7: Farming on `7 x 7` tile

### **Code:**
```python
clear()
do_a_flip()
move(South)

# variables
num_watertank = 100
num_hay = 40000
num_wood = 35000
num_carrots = 35000
num_pumpkins = 20000
num_power = 1000

pedalList = list()
# Main loop
while True:
	for i in range(get_world_size()):
		# Buy seeds if needed
		if num_items(Items.Sunflower_Seed) < 100:
			trade(Items.Sunflower_Seed, get_world_size())
		if num_items(Items.Carrot_Seed) < 100:
			trade(Items.Carrot_Seed, get_world_size())
		if num_items(Items.Pumpkin_Seed) < 100:
			trade(Items.Pumpkin_Seed, get_world_size())
			
		move(North)
		x = get_pos_x()
		y = get_pos_y()

		# Harvest Sunflowers
		if can_harvest():
			if get_entity_type() == Entities.Sunflower:
				if measure() == max(pedalList):
					harvest()
					pedalList.remove(max(pedalList))
			else:
				# Harvest, Water, and Plant
				harvest()
				watering()
				planting()
		else:
			if get_ground_type() == Grounds.Soil:
				till()
				
	# Move to the next row
	move(East)
```

### **Explanaton:**

In this part of the code, I’m using `pedalList` as a way to keep track of my sunflowers’ progress. Every time I plant a sunflower, I immediately measure it using `measure()` and add that value to `pedalList`. This gives me a list of all my sunflowers’ growth levels, which helps me know which ones are ready for harvesting. 

When I come across a sunflower that can be harvested, I only harvest it if its growth level matches the highest value in `pedalList` —meaning it’s one of the most mature in the field. After I harvest it, I remove its measurement from `pedalList`, so my list stays up-to-date with the sunflowers I have left. This way, I’m maximizing yield by only picking the most fully-grown sunflowers!




### **Note:**
- Unlocked utilities so that I can use `min()`, `max()`, `abs()` and `random()` functions. 
- In this step I focused mainly on what I want to track, which are;
    *  Position of the `Drone`
    * Position of the `Sunflower` with the most petals to yield more power


## Step 8: Farming on `9 x 9` tile

### **Code:**
```python
clear()
do_a_flip()
move(South)

# variables
num_watertank = 100
num_hay = 40000
num_wood = 45000
num_carrots = 45000
num_pumpkins = 40000
num_power = 3500

pedalList = list()
# Main loop
while True:
	for i in range(get_world_size()):
		#buy stuffs
		buying()
		#move
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		#Harvesting and watering
		harvesting()
		
	# Move to the next row
	move(East)

def harvesting():
	# Harvest Sunflowers
		if can_harvest():
			if get_entity_type() == Entities.Sunflower:
				if measure() == max(pedalList):
					harvest()
					pedalList.remove(max(pedalList))
			else:
				# Harvestand Plant
				harvest()
				planting()
			# Use water if water level is below 75%
			if get_water() < 0.8:
				use_item(Items.Water_Tank)
		else:
			if get_ground_type() == Grounds.Soil:
				till()

def planting():
	# Sunflower
	if num_items(Items.Power) < num_power:
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Sunflower)
		pedalList.append(measure())
	
	# Hay 
	elif num_items(Items.Hay) < num_hay:
		if get_ground_type() == Grounds.Soil:
			till()
		plant(Entities.Grass)
				
	# Wood 
	elif num_items(Items.Wood) < num_wood:
		if (x % 2 == 0 and y % 2 == 1) or (x % 2 == 1 and y % 2 == 0):
			plant(Entities.Tree)
		else:
			if get_ground_type() == Grounds.Soil:
				till()
			plant(Entities.Bush)
	
	# Carrots
	elif num_items(Items.Carrot) < num_carrots:
		if num_items(Items.Carrot_Seed) == 0:
			trade(Items.Carrot_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Carrots)
		
	# Pumpkins
	elif num_items(Items.Pumpkin) < num_pumpkins:
		if num_items(Items.Pumpkin_Seed) == 0:
			trade(Items.Pumpkin_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Pumpkin)


def watering():
	# Check water tank inventory and refill if low
	if num_items(Items.Water_Tank) < num_watertank:
		trade(Items.Empty_Tank, 5)
	

def buying():
	# Buy seeds if needed
		if num_items(Items.Sunflower_Seed) < 100:
			trade(Items.Sunflower_Seed, get_world_size())
		if num_items(Items.Carrot_Seed) < 100:
			trade(Items.Carrot_Seed, get_world_size())
		if num_items(Items.Pumpkin_Seed) < 100:
			trade(Items.Pumpkin_Seed, get_world_size())
		if num_items(Items.Fertilizer) < 100:
			trade(Items.Fertilizer, get_world_size())
```

### **Note:**
- This code is updated code where I grouped the planting functions all in the new function called `harvesting`.
- Here I tried to farm as much as possible and upgraded everything I can from the yield of my harvest.
- In order to collect more resources so I need to expand the size to `9 x 9` from `7 x 7`


## Step 9: Farming on `10 x 10` tile

### **Code:**
```python
clear()
do_a_flip()
move(South)

# variables
num_watertank = 100
num_hay = 100000
num_wood = 60000
num_carrots = 60000
num_pumpkins = 80000
num_power = 200

pedalList = list()
# Main loop
while True:
	for i in range(get_world_size()):
		#buy stuffs
		buying()
		#move
		move(North)
		x = get_pos_x()
		y = get_pos_y()
		#Harvesting and watering
		harvesting()
		
	# Move to the next row
	move(East)


def harvesting():
	# Harvest Sunflowers
		if can_harvest():
			if get_entity_type() == Entities.Sunflower:
				if measure() == max(pedalList):
					harvest()
					pedalList.remove(max(pedalList))
			#create maze
			elif get_entity_type() == Entities.Bush and num_items(Items.Wood) > num_wood:
				use_item(Items.Fertilizer)
			#solve the maze
			elif get_entity_type() == Entities.Hedge:
				SolveMaze()
			#Harvesting
			else:
				# Harvestand Plant
				harvest()
				planting()
			# Use water if water level is below 75%
			if get_water() < 0.8:
				use_item(Items.Water_Tank)
		else:
			if get_ground_type() == Grounds.Soil:
				till()


def planting():
	# Sunflower
	if num_items(Items.Power) < num_power:
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Sunflower)
		pedalList.append(measure())
	
	# Hay 
	elif num_items(Items.Hay) < num_hay:
		if get_ground_type() == Grounds.Soil:
			till()
		plant(Entities.Grass)
				
	# Wood 
	elif num_items(Items.Wood) < num_wood:
		if (x % 2 == 0 and y % 2 == 1) or (x % 2 == 1 and y % 2 == 0):
			plant(Entities.Tree)
		else:
			if get_ground_type() == Grounds.Soil:
				till()
			plant(Entities.Bush)
	
	# Carrots
	elif num_items(Items.Carrot) < num_carrots:
		if num_items(Items.Carrot_Seed) == 0:
			trade(Items.Carrot_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Carrots)
		
	# Pumpkins
	elif num_items(Items.Pumpkin) < num_pumpkins:
		if num_items(Items.Pumpkin_Seed) == 0:
			trade(Items.Pumpkin_Seed, 5)
		if get_ground_type() == Grounds.Turf:
			till()
		plant(Entities.Pumpkin)
		
	#maze
	else:
		if get_ground_type() == Grounds.Soil:
			till()
		plant(Entities.Bush)
		

def buying():
	# Buy seeds if needed
		if num_items(Items.Sunflower_Seed) < 100:
			trade(Items.Sunflower_Seed, get_world_size())
		if num_items(Items.Carrot_Seed) < 100:
			trade(Items.Carrot_Seed, get_world_size())
		if num_items(Items.Pumpkin_Seed) < 100:
			trade(Items.Pumpkin_Seed, get_world_size())
		if num_items(Items.Fertilizer) < 100:
			trade(Items.Fertilizer, get_world_size())
	

def watering():
	# Check water tank inventory and refill if low
	if num_items(Items.Water_Tank) < num_watertank:
		trade(Items.Empty_Tank, 5)
	


def SolveMaze():
	direction = North
	while get_entity_type() != Entities.Treasure:
		direction = TurnLeft(direction)
		if move(direction) == False:
			direction = TurnRight(direction)
		if move(direction) == False:
			direction = TurnRight(direction)
		else:
			direction = TurnLeft(direction)
			if move(direction) == False:
				direction = TurnRight(direction)
				
	harvest()


def TurnRight(direction):
	if direction == North:
		return East
	elif direction == East:
		return South
	elif direction == South:
		return West
	else:
		return North
	
def TurnLeft(direction):
	if direction == North:
		return West
	elif direction == West:
		return South
	elif direction == South:
		return East
	else:
		return North
```

### **Explanation:**

In this code, I’m navigating a maze to reach a treasure. The function `SolveMaze()` and the helper functions `TurnRight()` and `TurnLeft()` handle my movement through the maze by adjusting my direction and ensuring I can reach the goal. Let’s break down each part.

### `SolveMaze()`

1. **Starting Direction**:
   - I set my initial direction to `North`. This will be my reference point as I move.

2. **Looping Through the Maze**:
   - The loop keeps running until I reach the treasure (when `get_entity_type() == Entities.Treasure`), which will break out of the loop once found.
   - Inside the loop, I try moving forward by turning left first, following a left-hand rule for the maze.

3. **Checking for Movement**:
   - I first turn left (calling `TurnLeft()`), and if moving in that direction isn’t possible (`move(direction) == False`), I switch to turning right to find an alternative route.
   - If turning right also doesn’t work, I try turning right again. If still stuck, I turn left once more as a last option.
   - This sequence ensures I try every possible option for moving forward, following walls on my left side until I reach the treasure.

### `TurnRight()` and `TurnLeft()`

- **Turning Right**:
   - `TurnRight(direction)` takes my current direction and updates it by rotating 90 degrees clockwise. 
   - For example, if I’m facing North and turn right, I’ll be facing East, then South, and so on, cycling through each direction.
   
- **Turning Left**:
   - `TurnLeft(direction)` rotates my direction 90 degrees counterclockwise.
   - For instance, if I’m facing North and turn left, I’ll end up facing West, then South, and so forth.

With these functions, I’m able to navigate the maze by continuously adjusting my direction and moving along the walls, ensuring I systematically explore all paths until I find the treasure. The left-hand rule, along with checking both left and right turns, helps me avoid getting stuck and ensures I’ll eventually reach my goal.





# Challenges-and-Learnings
## Challenges I faced
In this game, each stage presented its own set of unique challenges. Here’s a rundown of the main obstacles I faced:

1. **Harvesting Sunflowers**:
   - Sunflowers were tricky to harvest because they needed to be fully matured, and I had to track each one’s growth. I used a list (`pedalList`) to keep track of each sunflower’s growth level by adding a “measure” value for each planted sunflower. This allowed me to know when a sunflower reached its maximum growth, but it required constant attention to make sure I wasn’t harvesting too early. If I missed updating this list accurately, I’d end up with smaller yields and wasted resources.

2. **Managing Power Levels**:
   - Maintaining sufficient power was essential for farming. Planting and harvesting, as well as navigating the maze, required power, and balancing this resource with the seeds and water tank levels was critical. Running out of power mid-task could interrupt progress, especially when I had several sunflowers or other crops to tend to. 

3. **Tilling the Ground**:
   - Tilling required more precision than expected. Certain crops could only grow in specific ground types (like turf for sunflowers and carrots), and I had to ensure the soil was correctly prepared before planting. If I failed to till correctly, seeds wouldn’t take, and I’d have to start over on that patch of ground. Timing tilling operations with planting was essential for a steady crop cycle.

4. **Navigating the Maze**:
   - The maze was one of the most complex parts of the game. Using the `SolveMaze()` function, I navigated with a left-hand rule approach, carefully choosing each direction and testing each route to avoid dead ends. This required a methodical approach and patience, especially when encountering obstacles like bushes, which I could fertilize to create paths, or hedges that added to the challenge.



## Learnings
   Through the challenges in this game, I’ve gained valuable insights and built a strong foundation in Python programming:

1. **Understanding Conditional Logic**:
   - Navigating the maze with directional functions (`TurnLeft`, `TurnRight`, and `SolveMaze`) taught me how to structure and implement conditional statements. I had to decide on specific actions based on conditions like the current direction or entity type. This practical use of `if` statements has deepened my understanding of logical flow in Python.

2. **Working with Lists**:
   - By using `pedalList` to keep track of sunflower growth stages, I practiced list operations in Python. This taught me how to add, retrieve, and remove items, which is fundamental for data management in many applications. Understanding lists is helping me with larger projects where I need to store and manipulate multiple values.

3. **Resource Management**:
   - Balancing items like seeds, water, and power required a thoughtful approach to variables and functions. Writing code that checked inventory, traded items, and kept track of supplies enhanced my understanding of variables and loops. I can now see how tracking resources in games parallels managing data in real-world scenarios.

4. **Function Creation and Modular Code**:
   - By creating functions like `watering()`, `harvesting()`, and `planting()`, I learned to keep code organized and modular. This makes it easier to update or debug specific parts of my code without affecting the whole program. Now, I understand why developers break down tasks into smaller functions to make code more readable and reusable.

5. **Debugging and Patience**:
   - Encountering issues, like failing to harvest sunflowers or struggling with tilling timing, has taught me to carefully read error messages and systematically identify problems. This skill is critical in any programming language, as it builds patience and a problem-solving mindset.

Overall, this game has been a hands-on way to practice Python fundamentals and gain confidence in using the language effectively.


# References
1. CODE, FARM, AUTOMATE: The Farmer Was Replaced - Programming a Drone (Video Game) 
- link:  https://youtu.be/gmJ357XAAdE?si=BZ3StRy0Zb6Ak6jm

2. Professional Programmer codes an optimized AI | The Farmer Was Replaced
- link:  https://youtu.be/QvtNVxjkc9U?si=0nramRizeXGAPlxA