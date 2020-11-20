# Daa Assignement 1

# Brute force algorithm

Basic idea:
 
The basic idea of the brute force algorithm is to place the queens on all possible positions and check each time if the queens cannot capture each other. If not then it has found a solution. Because of the vast amount of possible positions (NN for a table of size N while each row has 1 queen), this algorithm is not practical even for small table sizes (like N=12).
 
 
 
# Advantages over other methods:
 
Probably none. The brute force algorithm is only mentined to point out the superiority of the other algorithms, as a brute force approach is the last resort, when every other attempt failed.
 
 
 
# Other thoughts:
 
But after "forcing" the algorithm to place only one queen on each row and one on each column the number of posible valid positions decreases to N! (N!=1*2*3....*(N-1)*N). Using this algorithm we can found a solution for larger table sizes compared to the previous method (like N=17).
 
I will not present an actual brute force algorithm here because it is not practical (has exremely low speed due to the enormous amount of resources-calculations required).

# Backtracking algorithm

# Basic idea
An N Queens backtracking algorithm is much more efficient by any brute force approach. The idea is to place one queen on one edge and then continue by placing the next queen on the first valid position (in the next row / column) and so on. When no more queens can be placed the algorithm has either found a solution (if all queens are placed) or it needs to remove the processed queen and move the previous one to the next valid position. When a queen has been placed on the last valid position in a row / column and needs to be replaced it must be removed and the previous one must be moved to the next valid position.
 
If the previous explanation was too confusing, you can view each step separated bellow.

# Algorithm steps:

In the following lines I explain the backtracking algorithm in detail. More specifically this algorithm begins placing a queen to the upper line of the table and continues by moving to the bottom. The steps of the algorithm are listed by the order of execution unless specified otherwise.
 
Place the first queen in the left upper corner of the table.
Save the attacked positions.
Move to the next queen (which can only be placed to the next line).
Search for a valid position. If there is one go to step 8.
There is not a valid position for the queen. Delete it (the x coordinate is 0).
Move to the previous queen.
Go to step 4.
Place it to the first valid position.
Save the attacked positions.
If the queen processed is the last stop otherwise go to step 3.
 
The algorithm presented cannot be turned immediately in a structured program. But the only thing needed to do so is the addition of an infinite loop that includes steps 3 to 10 and can only be stopped by step 10.

# Details
One important detail of the backtracking algorithm is the function that saves the attacked positions (marks the invalid locations for the rest of the queens). This is the part of the algorithm that mostly determines its speed and efficiency. You can see the major difference of the two methods mentioned in the algorithm results - speed section.

<li>
<ol>
  One novice approach is to mark queens positions on a 2 dimentional matrix (array in programming). Zero should represent no threat (valid spot) whereas every other number of that matrix means invalid location. When the algorithm must place a queen the diagonals, rows / columns and lines it threatens should take the number of the line of that queen (unless they already are not zero because another queen also threatens them). When the algorithm must remove a queen of the line k all the numbers of the matrix that are equal to k should become zero (numbers equal to k are those that are threatened just by the k queen so when this queen is removed they should become zero (no threat)). You can download this version of the algorithm here.
  <ol>
<ol>
  Another method is to save just the row / column and the diagonals that each queen occupies. The rows  / columns can be saved on a boolean one dimentional array / matrix with true meaning occupied row / column and false meaning free row / column. The diagonals can be also saved on two boolean one dimentional array / matrix and accessed with x - y and x + y numbers (where x is the number of the row / column of the queen and y is the number of the line). The upper left queen has x = 1 and y = 1 and the lower right queen has x = N and y = N for a table size of N). The diagonals accesed with x - y are those with positive slope whereas x + y accessed the negative slope diagonals. The second method along with other minor optimizations yields a 20x times speed up over the first (method). You can download this version of the algorithm here.
  <ol>
<ol>
  The last and probably the best way of marking queens positions is using bitfields which will not be expained in this site. However the speed penalty of using the second method over the third is less than the penalty of using the first over the second method.
  <ol>
   
<li>
  Also the backtracking algorithm time complexity is exponential. 
  
  # Advantages over other methods:
The major advantage of the backtracking algorithm is the abillity to find and count all the possible solutions rather than just one while offering decent speed. In fact this is the reason it is so widely used. Also one can easily produce a parallel version of the backtracking algorithm increasing speed several times just by starting multiple threads with different starting positions of the first queens.

# Other thoughts:
The backtracking algorithm can be further optimised by using bitfields. You can study Jeff Somers's solution to the N Queens problem for further details. Also the backtracking algorithm can be easilly implemented on a GPU or a Multicore CPU. However it cannot find any solutions in a logical amount of time (some days) for numbers greater to 60 - 100 due to the exponential increase of the time needed as N (table size) grows.
