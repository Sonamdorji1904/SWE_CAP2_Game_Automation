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


## Step 2: Farming on `3 x3` tile

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