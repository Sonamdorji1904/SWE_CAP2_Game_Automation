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
- [Code Snippets and Explanation](###code-snippets-and-explanation)
- [Challenges and Learnings](#challenges-and-learnings)
- [References](#references)

 ## Code-Snippets-and-Explanation

### Step 1
**Code:**

```python
harvest()
```
**Explanation:**

The code runs and collects grass upto 5 and then the loops get unlocked
**Demo:**

![Step_1](./Game1.mp4)

```python
while True:
    if can_harvest():
        harvest()
    else:
        do_a_flip()
```
**Explanation:**

The code runs an infinite number of times and harvest the grass if the condition is true and else the drone does a flip and continue harvesting.

```python
while True:
    if can_harvest():
        harvest()
        move(North)
```
**Explanation:**

After expanding our tiles to `3 x 1` then while  

