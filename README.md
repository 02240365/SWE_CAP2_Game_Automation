# Programming the Farming Drone (Report)

## Introduction

In the Farmer is Replaced Python game, players take on the role of an automated farming drone tasked with managing various crops and resources on a grid-like farm. Unlike a typical farming game where players control a character directly, here the player’s job is to write Python code that directs the drone to perform tasks such as planting, watering, harvesting crops, and collecting treasures or resources like wood.

### Game Objective
The primary objective of the game is to efficiently manage resources to meet specific quotas or objectives, like harvesting a set amount of certain crops (e.g : carrots, hay) or locating and collecting treasure items scattered across the grid. Players need to automate tasks by writing functions and loops to optimize the drone’s actions, ensuring it makes the best use of time and resources while navigating the farm grid.

Through code, players can manage:

**Planting and Harvesting**: Directing the drone to plant, water, and harvest crops in an organized manner.

**Collecting Treasures**: Exploring the grid to find and collect treasures that provide additional resources or rewards.

**Resource Management**: Trading or using resources like seeds and water to maintain and expand the farm.



# Table of Contents
-[Code Snippets and Explanation](#code-snippets-and-explanation)

-[Challenges and Learnings](#challenges-and-learnings)

-[References](#references)



## Step 1 : Farming on 1 Tile

**Code**

```python
whileTrue:
    if can_harvest():
        harvest()
```

**Explanation**

The code runs an infinite number of times and harvest the grass with the if condition.


**Demo**

Video Demo :

https://github.com/user-attachments/assets/144c57d6-9d2a-41a0-b874-6317dfd4e8a5


**Notes**

- Using the code above I was able to get enough hay to unlock the tile.

- These features were unlocked too : variables and functions.





## Step 2 : Planting a Bush

**Code**

```python
whileTrue:
    if can_harvest():
        harvest()
    else:
        plant(Entities.Bush)
        do_a_flip()
```

**Explanation**

The code makes the drone go one square at a time harvests the grass with the if condition and plants a bush after harvesting the grass.

**Demo**

Video Demo :


https://github.com/user-attachments/assets/7b84805b-f0b1-4866-92bb-8b6ee015b652



**Notes**

- Using the code above I was able to get enough wood to unlock the speed and operators.




## Step 3 : Farming on 3x3 Tile

**Code**

```python
while True:
	for x in range(get_world_size()):
		move(East)
		trade(Items.Carrot_Seed)
		for y in range(get_world_size()):
			if num_items(Item.Carrot):
				if can_harvest():
					harvest()
                    till()
				    plant(Entities.Carrots)
				move(South)
            else:
                retuen
```

**Explanation**
This code continuously moves across a 3x3 grid, trading for carrot seeds, planting and harvesting carrots if possible, and stopping if no carrots are available.

**Demo**

Video Demo :

https://github.com/user-attachments/assets/1ce28eca-81f1-4bcb-9e18-3bbadb9bb20c


**Notes**

- Using the code above I was able to harvest wood and hay simultaneously.







## Step 4 : Planting Grass

**Code**

```python
def plant_grass(req):
	
	# water percentage for grass is low because grass grows quick

	WATER_PERCENT = .25
	
	reset_drone()
	
	while num_items(Items.Hay) < req:
		
		# loop entire grid
		for x in range(get_world_size()):
			for y in range(get_world_size()):
				
				water_me(WATER_PERCENT)
			
				if can_harvest():
					harvest()
				plant(Entities.Grass)
				move(South)
			move(East)
		
```

**Explanation**

This code makes the drone to plant and harvest grass across the grid, applying minimal water each time, until the required amount of hay is collected.

**Demo**

Video Demo :

https://github.com/user-attachments/assets/7e187659-a38b-46b0-969f-9819a25cba2b


**Notes**

- Using the code above I was able to get huge amount hay to unlock expensive functions and upgrade speed and I could even expand the field.




## Step 5 : Planting Trees

**Code**

```python
def plant_trees(req):
	while num_items(Items.wood) < req:
		for x in range(get_world_size()):
			for y in range(get_world_size()):
				water_me(.75)
				if (x+y) % 2 == 0:
					if can_harvest():
						harvest()
					plant(Entities.Tree)
				else:
					if can_harvest():
						harvest()
					plant(Entities.Bush)
				move(South)
			move(East)
```

**Explanation**

This code plants trees and bushes in a checkerboard pattern across the grid, watering each cell, and harvesting as needed until the required amount of wood is collected.

**Demo**

Video Demo :


https://github.com/user-attachments/assets/208b2564-60cc-424e-812d-456dafeebab8


**Notes**

- Using the code above I was able to get five woods at time which unlocked a lot of features quickly and saved a lot of time.



## Step 6 : Planting Carrots

**Code**

```python
def plant_carrots(req):
	
	# water percent for carrots

	WATER_PERCENT = .65
	
	reset_drone()
	
	while num_items(Items.Carrot) < req:
		
		# loop entire grid
		for x in range(get_world_size()):
			for y in range(get_world_size()):
				
				# checking if there is enough carrot seeds
				while not trade_req(Items.Carrot_Seed, 5):
					plant_grass(500)
					plant_trees(500) 
				
				water_me(WATER_PERCENT)
				
				# condition to exit
				if num_items(Items.Carrot) < req:
					if can_harvest():
						harvest()
					if get_ground_type() != Grounds.Soil:
						till()
					plant(Entities.Carrots)
					move(South)
			move(East)
		
```

**Explanation**


This code makes the drone to plant, water, and harvest carrots across the grid, trading for carrot seeds as needed and planting other crops if seeds are insufficient, until the required number of carrots is collected.

**Demo**

Video Demo :


https://github.com/user-attachments/assets/e40aa6ba-50c7-416f-ba96-9c890e5a1fbd




**Notes**

- Using the code above I was able to get enough carrots to unlock other vegetables and plants.




## Step 7 : Planting Pumpkin

**Code**

```python
def plant_pumkins(req):
	TOTAL_GRID = get_world_size() * get_world_size()
	
	checks = 0
	reset_drone()
	harvest_grid()
	while num_items(Items.Pumpkin) < req:
				
				for x in range(get_world_size()):
					for y in range(get_world_size()):
						if get_entity_type() != Entities.Pumpkin and not get_entity_type() == None:
							harvest()
						else:
							while not trade_req(Items.Pumpkin_Seed, 5):
								plant_carrots(50)
								reset_drone()
								harvest_grid()
							water_me(.75)
							plant(Entities.Pumpkin)	
						move(South)
					move(East)
				
				
					coord_list = []
					for x in range(get_world_size()):
						for y in range(get_world_size()):
							if get_entity_type() != Entities.Pumpkin:
								coord_list.append([get_pos_x(), get_pos_y()])
								while not trade_req(Items.Pumpkin_Seed, 5):
									plant_carrots(50)
									reset_drone()
									harvest_grid()
								water_me(.75)
								plant(Entities.Pumpkin)
							move(South)
						move(East)
					while True:
						temp_coord = []
						coord_list = []

						for coord in coord_list:
							goto(coord[0],coord[1])
							if get_entity_type() != Entities.Pumpkin:
								temp_coord.append(coord)
								while not trade_req(Items.Pumpkin_Seed, 5):
									plant_carrots(50)
									reset_drone()
									harvest_grid()
								water_me(.75)
								plant(Entities.Pumpkin)
								
						coord_list = temp_coord
						if not temp_coord:
							while True:
								if can_harvest():
									harvest()
									break
							break
							       
							
							
					
		
```

**Explanation**



This code makes the drone to plant and harvest pumpkins by traversing the grid, checking and recording empty cells, trading for seeds as needed, replanting at unoccupied positions, and iteratively revisiting and replanting until the required number of pumpkins is collected.

**Demo**

Video Demo :

https://github.com/user-attachments/assets/ae2cec7a-ca1d-44eb-bc27-8a928ad1001e


**Notes**

- Using the code above I was able to get enough pumpkin to unlock advanced and useful data types which made the coding much simpler and shorter.




## Step 8 : Planting Sunflower

**Code**

```python
def plant_sunflowers(req):
	
	# water percent for sunflower

	WATER_PERCENT = .65
	
	reset_drone()
	
	while num_items(Items.Power) < req:
		reset_drone()

		
		# loop entire grid
		for x in range(get_world_size()):
			for y in range(get_world_size()):
				
				# checking if there is enough carrot seeds
				while not trade_req(Items.Sunflower_Seed, 5):
					plant_carrots()
	
				
				water_me(WATER_PERCENT)
				
				# condition to exit
				if num_items(Items.Power) < req:
					if can_harvest():
						harvest()
					if get_ground_type() != Grounds.Soil:
						till()
					plant(Entities.Sunflower)
					move(South)
			move(East)
		
		max_petals = 0
		list_petals = []
		coords = []
		for x in range(get_world_size()):
			for y in range(get_world_size()):
				num_petals = measure()
				if num_petals == None:
					list_petals.append(0)
				else:
					list_petals.append(num_petals)
				coords.append([get_pos_x(), get_pos_y()])
				move(South)
			move(East)
				
			
		num_maxes = 0
		while num_maxes <= len(list_petals) -1:
			max_petals = max(list_petals)
			count = 0
			for numpetals in list_petals:
				if numpetals == max_petals:
					list_petals.pop(count)
					break
				count += 1
			goto(coords[count][0], coords[count][1])
			coords.pop(count)
			harvest()
			num_maxes += 1
			
				
				
				
```

**Explanation**


This code guides the drone to plant, water, and harvest sunflowers across the grid, trading for seeds if needed, and later measures, locates, and harvests sunflowers with the maximum petals until the required power level is achieved.

**Demo**

Video Demo :


https://github.com/user-attachments/assets/7f6e311a-7437-4fc9-b976-d48219136cca



**Notes**

- Using the code above I was able to get enough sunflower to unlock lower level of the games like maze, treasure and fertilizers.



## Step 9 : Treasure Harvesting

**Code**

```python
def coord():
	return[get_pos_x(), get_pos_y()]
directions = [North, East, South, West]
x = 0

while True:
	plant(Entities.Bush)
	do_a_flip()
	do_a_flip()
	do_a_flip()
	do_a_flip()
	while get_entity_type() != Entities.Hedge:
		use_item(Items.Fertilizer)

	for i in range(10):
		visited = []
		while get_entity_type() != Entities.Treasure:
			
			while not move(directions[x]):
				quick_print(directions[x])
				x += 1
				if x == 4:
					x = 0
				
			x -= 1
			if x == -1:
				x = 3
				
				
		while get_entity_type() == Entities.Treasure:
			while not trade_req(Items.Fertilizer, 5):
				harvest()
				plant_pumkins(10000)
			use_item(Items.Fertilizer)
	harvest()
	
	
```

**Explanation**
This code defines a loop where an entity plants bushes, navigates to treasures while using fertilizer, and trades for items, repeating the process indefinitely.


**Demo**

Video Demo :

https://github.com/user-attachments/assets/6c2e126b-d541-4c16-b254-728823c81d91



**Notes**

- Using the code above I was able to get Treasure to unlock cactus.




## Step 10 : Planting Cactus

**Code**

```python
def reverse(dir):
	if dir == South:
		move(North)
	elif dir == North:
		move(South)
	elif dir == West:
		move(East)
	elif dir == East:
		move(West)

def check_direction(dir):
	move(dir)
	m = measure()
	reverse(dir)
	return(m)

reset_drone()
while True:
	for x in range(get_world_size()):
		for y in range(get_world_size()):
			if get_entity_type() != Entities.Cactus:
				plant(Entities.Cactus)
			move(South)
		move(East)
	count = 0
	while count != 5:
		for x in range(get_world_size()):
			for y in range(get_world_size()):
				current_cactus = measure()
				if on_edge(get_pos_x(), get_pos_y()):
					if x == 0:
						size = check_direction(West)
						if size > current_cactus:
							
							swap(West)
								
						for dir in [North, East]:
							size = check_direction(dir)
							if size < current_cactus:
							
								swap(dir)
						
						# not going south
					if y == 0:
						size = check_direction(South)
						if size > current_cactus:
							swap(South)
								
						
						for dir in [North, East]:
							size = check_direction(dir)
							if size < current_cactus:
								swap(dir)
							
						# not going west
					if x == get_world_size() -1:
						for dir in [South, West]:
							size = check_direction(dir)
							if size > current_cactus:
									
								swap(dir)
								
						size = check_direction(East)
						if size < current_cactus:
						
							swap(East)
								
						# not going north
					if y == get_world_size() -1:
						for dir in [South, West]:
							size = check_direction(dir)
							if size > current_cactus:
									
								swap(dir)
								
						size = check_direction(North)
						if size < current_cactus:
								
							swap(North)
								
								
							# not going east
				else:
					for dir in [South, West]:
						size = check_direction(dir)
						if size > current_cactus:
								
							swap(dir)
								
						
					for dir in [North, East]:
						size = check_direction(dir)
						if size < current_cactus:
							
							swap(dir)
						
					move(South)
				move(East)
			count += 1
			
	harvest()
	reset_drone()
	
	
```

**Explanation**
This code makes the drone  to navigate a grid-like world, checking the size of cacti in its vicinity, planting new cacti where necessary, and attempting to optimize its position based on cactus size, all while ensuring it does not move out of bounds.


**Demo**

Video Demo :

https://github.com/user-attachments/assets/fa58eb3a-e4a9-4ca0-b9db-5cad93e6f21a


**Notes**

- Using the code above I was able to harvest cactus and unlock dinosaur.




# Challenges and Learnings

## Challenges

In the Farmer is Replaced Python game, several challenges made gameplay both engaging and complex:

**1.Efficient Resource Management**: Balancing resources like seeds and water while meeting crop quotas requires careful planning and prioritization. Running out of seeds or water at the wrong time can disrupt the workflow and require backtracking to collect or trade for more.

**2.Grid Navigation**: Programming the drone to navigate the grid efficiently, especially with constraints on movement direction and positioning, is a challenge. Looping across the grid without missing cells or revisiting already-harvested spots requires precise logic.

**3.Conditional Logic for Mixed Actions**: Many tasks involve multi-step sequences (e.g., planting, watering, harvesting) with conditions, such as only planting specific crops in designated soil types or swapping to a fallback crop if resources are insufficient. Coding these steps with minimal redundancy demands effective use of loops and conditionals.

**4.Avoiding Infinite Loops and Recursion**: Some tasks, like replanting when resources are low, can lead to infinite loops if not handled carefully. Implementing checks to break out of loops and prevent unintended recursive calls is crucial.

**5.Prioritizing High-Yield Harvests**: When faced with limited resources, choosing which crops to prioritize (such as high-yield crops like pumpkins) adds strategic depth. Measuring factors like yield and growth time becomes essential to maximize output within constraints.




## Learnings

Playing and solving Farmer is Replaced provided valuable insights and learning experiences in several areas:

**1.Optimizing Code for Efficiency**: The game taught the importance of writing clean, efficient loops and conditionals to navigate the grid, reducing redundant actions and optimizing the drone’s path to save resources and time.

**2.Resource Management and Planning**: Balancing limited resources like seeds, water, and crop yields highlighted the need for strategic planning. This required understanding when to trade, plant, or harvest specific crops to meet requirements without waste.

**3.Conditional Logic and Problem Solving**: The complex, multi-step tasks involving conditional actions (e.g., harvesting only when crops are ready, switching to fallback crops) improved understanding of nested conditions and recursive functions, which are essential for advanced coding logic.

**4.Debugging and Avoiding Infinite Loops**: Encountering infinite loops or unexpected recursion due to resource shortages underscored the importance of setting clear exit conditions and using error handling to maintain control flow.

**5.Grid-Based Movement and Coordination**: Developing precise algorithms to direct the drone across the grid and handle edge cases (like boundaries or revisiting cells) was a practical exercise in spatial reasoning and algorithm design.



## References

1.[Olexa](youtube.com/channel/UC_l-VTgITlhdOqaff4LdCkw)

2.[Jack Hodkinson](www.youtube.com/@jack.hodkinson)

3.[Chatgpt](https://chatgpt.com)
