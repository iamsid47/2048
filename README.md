## 2048  
The legendary 2048 game using Python!

In this workshop, we will look python code and logic to design a 2048 game you have played very often in your smartphone. If you are not familiar with the game, it is highly recommended to first play the game so that you can understand the basic functioning of it.

## How to play 2048 :

1. There is a 4*4 grid which can be filled with any number. Initially two random cells are filled with 2 in it. Rest cells are empty.

2. We have to press any one of four keys to move up, down, left, or right. When we press any key, the elements of the cell move in that direction such that if any two identical numbers are contained in that particular row (in case of moving left or right) or column (in case of moving up and down) they get add up and extreme cell in that direction fill itself with that number and rest cells goes empty again.

3. After this grid compression any random empty cell gets itself filled with 2.

4. Following the above process we have to double the elements by adding up and make 2048 in any of the cell. If we are able to do that we wins.

5. But if during the game there is no empty cell left to be filled with a new 2, then the game goes over.

In above process you can see the snapshots from graphical user interface of 2048 game. But all the logic lies in the main code. So to solely understand the logic behind it we can assume the above grid to be a 4*4 matrix ( a list with four rows and four columns). *You can see below the way to take input and output without GUI for the above game*.

```
Commands are as follows : 
'W' or 'w' : Move Up
'S' or 's' : Move Down
'A' or 'a' : Move Left
'D' or 'd' : Move Right
[0, 0, 0, 0]
[0, 0, 0, 0]
[0, 0, 0, 0]
[0, 0, 2, 0]
Press the command : a
GAME NOT OVER
[0, 0, 0, 2]
[0, 0, 0, 0]
[0, 0, 0, 0]
[2, 0, 0, 0]
Press the command : s
GAME NOT OVER
[0, 0, 0, 0]
[0, 0, 0, 0]
[0, 0, 2, 0]
[2, 0, 0, 2]
Press the command : d
GAME NOT OVER
[0, 0, 0, 0]
[0, 0, 0, 0]
[2, 0, 0, 2]
[0, 0, 0, 4]
Press the command : a
GAME NOT OVER
[0, 2, 0, 0]
[0, 0, 0, 0]
[4, 0, 0, 0]
[4, 0, 0, 0]
Press the command : s
GAME NOT OVER
[0, 0, 0, 0]
[0, 0, 0, 0]
[0, 0, 0, 0]
[8, 2, 0, 2]
.
.
.
And the series of input output will go on till we lose or win!
```

## The Approach

We will design each logic function such as we are performing a left swipe then we will use it for right swipe by reversing matrix and performing left swipe.
Moving up can be done by taking transpose then moving left.
Moving down can be done by taking transpose the moving right.
All the logic in the program are explained in detail in the comments. Highly recommended to go through all the comments.

## The Python Files

We have two python files below, one is ```2048.py``` which contains main driver code and the other is ```logic.py``` which contains all functions used. `logic.py` should be imported in `2048.py` to use these functions. If you want to try this on a computer (and not on Repl.it), just place both the files in the same folder then run `2048.py`. Will work perfectly.


## Let's Get Started!

Let's head over to [Repl.it](https://repl.it) and create a new repl. Choose the language as Python and name your repl.

Now, first we want to import the *Random Library* into our `logic.py` file. This will be used to generate random numbers for our game.

## Part 1. `logic.py`

```python
import random 
```

Next, we create a function to initialize the game (aka the grid when we start the game.) After this, we'll be declaring an empty list then and *appending* **4 lists** each with **four elements** as **0**.

```python
# function to initialize game / grid 
# at the start 
def start_game(): 
  
    # declaring an empty list then 
    # appending 4 list each with four 
    # elements as 0. 
    mat =[] 
    for i in range(4): 
        mat.append([0] * 4)
```

Now, we need to print the controls for the user so that he can move up/down or sideways. For this we use `print`. We will have to create 4 commands.
  1. Move Up
  2. Move Down
  3. Move Left
  4. Move Right

```python
# printing controls for user 
    print("Commands are as follows : ") 
    print("'W' or 'w' : Move Up") 
    print("'S' or 's' : Move Down") 
    print("'A' or 'a' : Move Left") 
    print("'D' or 'd' : Move Right") 
```
Next, we need to call the function to add a **new 2 in** the grid after every step. Also, we need to add a **new 2** in the grid at any random empty cell.

```python
add_new_2(mat) 
    return mat 
    
def add_new_2(mat):
```
Let's choose a random index for the row and column.

```python
r = random.randint(0, 3) 
c = random.randint(0, 3)
```

Now we write the logic when this while loop will break as the random cell chosen will be empty (or contains a zero)

```python
while(mat[r] != 0): 
        r = random.randint(0, 3) 
        c = random.randint(0, 3)
```

We will also replace a 2 at that empty random cell.

```python
mat[r] = 2
```

So, after this, we create a function which gets us the current state of the game! In this function, we put an `if` statement that if any cell contains 2048 in it, we won!

```python
def get_current_state(mat): 
  
    # if any cell contains 
    # 2048 we have won 
    for i in range(4): 
        for j in range(4): 
            if(mat[i][j]== 2048): 
                return 'WON'
```

Also, there are chances that we are left with an empty cell! So, we create and `if` statement for this which will return the statement: **`Game Not Over`**

```python
for i in range(4): 
        for j in range(4): 
            if(mat[i][j]== 0): 
                return 'Game Not Over'
```

Now that's not the end! There is another condition where there is no empty cell but if we move left, right, up, or down, there can be a possibility that the 2 rows or columns get merged. For this, we again use `if` statemnent and return: `Game Not Over'

```python
for i in range(3): 
        for j in range(3): 
            if(mat[i][j]== mat[i + 1][j] or mat[i][j]== mat[i][j + 1]): 
                return 'GAME NOT OVER'
  
    for j in range(3): 
        if(mat[3][j]== mat[3][j + 1]): 
            return 'GAME NOT OVER'
  
    for i in range(3): 
        if(mat[i][3]== mat[i + 1][3]): 
            return 'GAME NOT OVER'
```

Lastly, we create the else statement where it returns the statement: `Lost`.

```python
return 'LOST'
```

Now we create the functions which are defined for the left swap initially. 

In this, now we create a function to compress the grid after every step before and  after merging cells. We name it: `compress`. Inside, `compress` we put a bool varialbe to determine if a change happened or not and set it initially to **False**.
After this, we create an empty grid and name it as `new_mat`.

```python
def compress(mat): 
changed = False
new_mat = []
for i in range(4): 
        new_mat.append([0] * 4)
```

Here we will shift entries of each cell to it's extreme left row by row loop to traverse rows.

```python
for i in range(4): 
        pos = 0
```

Now, we make the loop to traverse each column in respective row.

```python
for j in range(4): 
            if(mat[i][j] != 0):
```

Here, we again put an `if` statement for; if the cell is non empty then we will shift it's number to previous empty cell in that row denoted by pos variable. Lastly, we return new compressed matrix and the flag variable. 

```python
new_mat[i][pos] = mat[i][j] 
                  
                if(j != pos): 
                    changed = True
                pos += 1
return new_mat, changed
```

Next, we create a function to merge the cells in matrix after compressing. This application is similar just contains some tweaks. We name it: `merge`

```python
def merge(mat): 
      
    changed = False
      
    for i in range(4): 
        for j in range(3): 
  
            # if current cell has same value as 
            # next cell in the row and they 
            # are non empty then 
            if(mat[i][j] == mat[i][j + 1] and mat[i][j] != 0):
            
            # double current cell value and 
                # empty the next cell 
                mat[i][j] = mat[i][j] * 2
                mat[i][j + 1] = 0
  
                # make bool variable True indicating 
                # the new grid after merging is 
                # different. 
                changed = True
  
    return mat, changed 
```

Now, we create a function to reverse the matrix, meaning reversing the content of each row (reversing the sequence).

```python
def reverse(mat): 
    new_mat =[] 
    for i in range(4): 
        new_mat.append([]) 
        for j in range(4): 
            new_mat[i].append(mat[i][3 - j]) 
    return new_mat 
```

Next, there needs to be a function to get the transpose of matrix. Meaning, interchanging rows and columns.

```python
def transpose(mat): 
    new_mat = [] 
    for i in range(4): 
        new_mat.append([]) 
        for j in range(4): 
            new_mat[i].append(mat[j][i]) 
    return new_mat
```

Phew!~ Now, we create a function if we move left. Pretty similar though, but again; contains a few tweaks!

```python
# function to update the matrix 
# if we move / swipe left 
def move_left(grid): 
  
    # first compress the grid 
    new_grid, changed1 = compress(grid) 
  
    # then merge the cells. 
    new_grid, changed2 = merge(new_grid) 
      
    changed = changed1 or changed2 
  
    # again compress after merging. 
    new_grid, temp = compress(new_grid) 
  
    # return new matrix and bool changed 
    # telling whether the grid is same 
    # or different 
    return new_grid, changed 
  ```
  
  Next, we create the function if we move up.
  ```python
  # function to update the matrix 
# if we move / swipe right 
def move_right(grid): 
  
    # to move right we just reverse 
    # the matrix  
    new_grid = reverse(grid) 
  
    # then move left 
    new_grid, changed = move_left(new_grid) 
  
    # then again reverse matrix will 
    # give us desired result 
    new_grid = reverse(new_grid) 
    return new_grid, changed 
  ```
  
  And similarly functions for upward and downward movements.
 
 ```python
  # function to update the matrix 
  # if we move / swipe up 
   def move_up(grid): 
  
    # to move up we just take 
    # transpose of matrix 
    new_grid = transpose(grid) 
  
    # then move left (calling all 
    # included functions) then 
    new_grid, changed = move_left(new_grid) 
  
    # again take transpose will give 
    # desired results 
    new_grid = transpose(new_grid) 
    return new_grid, changed 
  
# function to update the matrix 
# if we move / swipe down 
def move_down(grid): 
  
    # to move down we take transpose 
    new_grid = transpose(grid) 
  
    # move right and then again 
    new_grid, changed = move_right(new_grid) 
  
    # take transpose will give desired 
    # results. 
    new_grid = transpose(new_grid) 
    return new_grid, changed 
```

## Part 2. `2048.py`

![Part 2 Starter Gif. LoL](https://media.giphy.com/media/jp7jSyjNNz2ansuOS8/giphy.gif)

First, we import the logic.py file where we typed the logic of our game. Next, we type in the driver code.

```python
import logic 
  
# Driver code 
if __name__ == '__main__':
```

Now, we call the `start_game` function and make a condition using `while`. Here, we will take in the user input for further steps like entering the command.
```python
while(True):
x = input("Press the command : ")
```

Next, we create an `if` statement for moving. Now, if we want to mow up, we create an `if` and enter in the commands for it. Next, we call the `move_up` function. After this, we get the current status and later print it.

```python
# we have to move up 
    if(x == 'W' or x == 'w'): 
  
        # call the move_up funtion 
        mat, flag = logic.move_up(mat) 
  
        # get the current state and print it 
        status = logic.get_current_state(mat) 
        print(status) 
```

Next, we again create an `if` statement for defining if the game is not over and add a new **2** else break this loop.

```python
if(status == 'GAME NOT OVER'): 
            logic.add_new_2(mat) 
  
# else break the loop  
    else: 
         break
```

The same step is to be done for moving down, left, and right.

```python
# to move down 
    elif(x == 'S' or x == 's'): 
        mat, flag = logic.move_down(mat) 
        status = logic.get_current_state(mat) 
        print(status) 
        if(status == 'GAME NOT OVER'): 
            logic.add_new_2(mat) 
        else: 
            break
  
    # to move left 
    elif(x == 'A' or x == 'a'): 
        mat, flag = logic.move_left(mat) 
        status = logic.get_current_state(mat) 
        print(status) 
        if(status == 'GAME NOT OVER'): 
            logic.add_new_2(mat) 
        else: 
            break
  
    # to move right 
    elif(x == 'D' or x == 'd'): 
        mat, flag = logic.move_right(mat) 
        status = logic.get_current_state(mat) 
        print(status) 
        if(status == 'GAME NOT OVER'): 
            logic.add_new_2(mat) 
        else: 
            break
```

Now, if the user presses an invalid key, we `print`: Invalid Key Pressed.

```python
else: 
        print("Invalid Key Pressed")
```

And lastly, we print this matrix after each move. For that:

```python
print(mat)
```

## Voila! You did it!

![You Did It](https://media.giphy.com/media/3oz8xAFtqoOUUrsh7W/giphy.gif)

## Hack It!

Start playing around with it. There's a lot of customization to this. For example, you can use the same `logic.py` used here and create your own python 2048 game using Pygame. Moreover, you can add in some visual designs like instead of numbers, make it other things like cake, berries, chocolate, candy, etc and define your stuff.

Perhaps, you can also make a block game with this. For example, the number *1* equals a yellow block. *2* equals a blue block and so on!

You can also make a **4096** instead of **2048**! The possibilites are endless ;)
