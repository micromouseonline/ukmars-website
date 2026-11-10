---
title: Maze solving in micro-python
date: '2025-11-01T20:06:48Z'
lastmod: '2025-11-09T17:38:49Z'
wp_id: 3991
---

The simplest algorithm for finding the best route through a maze uses the Flood Algorithm.

The code sections below will allow you to set up the arrays to hold the walls that are found and to generate the flood values for each cell of the maze using the flood algorithm.

## **Setting up the global and maze variables** {#Setting_up_the_global_and_maze_variables}

This section of code will define the constants relating to the size of the maze, the values put in each item in the walls array for the walls found on the 4 sides and finally the wall and maze arrays and processing list

```
WIDTH = 16 # is 16 in full size maze
HEIGHT = 16 # is 16 in full size maze
TABLEWIDTH = 16
TABLEHEIGHT = 16
START = 0 # the start cell number
MIDDLE = 135 # int((TABLEWIDTH * HEIGHT /2) + (WIDTH / 2)) # middle of full size maze
NORTH = 1
EAST = 2
SOUTH = 4
WEST = 8
VISITED = 16

# define size of maze cells 
# extra row added at top and one to right for processing at edge of maze
numcells = (TABLEWIDTH * (TABLEHEIGHT + 1)) + 10
# set up and initialise arrays for walls and flood values in maze
walls = [0]*numcells # array of cell items initialised to zero starting at cell 0
# walls[0] = 99   example of setting an indexed value 
maze = [0]*numcells # array that holds flood values for maze cells
# cells are numbers from left to right then upwards from start cell as zero
# to check bits in a byte use walls[n] & NORTH to check the north wall bit, walls[n] & EAST for next bit etc
proclist = [0]*numcells # array that holds the list of cells to be processed next by the flood routine
 
    
```

## This section of code will clear the flood table {#This_section_of_code_will_clear_the_flood_table}

Call it before performing a flood, so that we have an empty maze

```
def floodclear(): # clear the flood table
    global numcells    
    for x in range(256):
        maze[x] = numcells
```

## This section of code will flood the maze from the start cell to the finish cell.  {#This_section_of_code_will_flood_the_maze_from_the_start_cell_to_the_finish_cell}

It can be used to flood from the centre goal cell to the start when exploring towards the centre, or the other way round when returning to the start cell. Note the first line that helps to make the code run faster in this procedure

The flood routine will populate the flood table with a list of increasing numbers going from the start cell to the finish one. You can use this to identify a route from the start to the finish cell by following a path of cells whereby the flood number decreases by one

```
@micropython.native # run this routine in native mode (lower level code)
def floodmaze(strt,fin):   # flood the maze from the strt cell to the fin cell
    global maze, walls, floodfail, debug, numcells
    floodstart = time.ticks_ms() # get time now
    floodclear()           # clear the flood table to all 283
    floodcleared = time.ticks_ms() # get time now
    floodcleared = floodcleared - floodstart
    flooded = 0            # set flag to not finished flooding yet
    floodfail = 0          # flag to show if flood failed to complete to end point
    curr = strt            # current cell being processed
    floodval = 0
    maze[strt] = 1         # set start cell flood value to one
    n = 0   # index for processing list array of cells to say where to add to end of list
    nxt = 0                # pointer to the first unprocessed item on the list
    while (flooded == 0):
        fval = maze[curr]  # get current value of current cell
        if ((walls[curr] & SOUTH) == 0):     # is there a gap to the SOUTH of current cell
            if (maze[curr - TABLEWIDTH] == numcells):
                maze[curr - TABLEWIDTH] = fval + 1    # set flood value in this cell
                proclist[n] = curr-TABLEWIDTH    # save flood cell for future processing
                n = n + 1                        # update processing list number
                if (proclist[n-1] == fin):       # check if finished flooding
                    flooded = 1                  # set flag to stop loop
        if ((walls[curr] & EAST) == 0):      # is there a gap to the EAST of current cell
            if (maze[curr + 1] == numcells):
                maze[curr + 1] = fval + 1        # set flood value in this cell
                proclist[n] = curr + 1           # save flood cell for future processing
                n = n + 1                        # update processing list number
                if (proclist[n-1] == fin):           # check if finished flooding
                    flooded = 1                      # set flag to stop loop
        if ((walls[curr] & NORTH) == 0):     # is there a gap to the NORTH of current cell
            if (maze[curr + TABLEWIDTH] == numcells):
                maze[curr + TABLEWIDTH] = fval + 1    # set flood value in this cell
                proclist[n] = curr + TABLEWIDTH  # save flood cell for future processing
                n = n + 1                        # update processing list number
                if (proclist[n-1] == fin):           # check if finished flooding
                       flooded = 1                      # set flag to stop loop
        if ((walls[curr] & WEST) == 0):      # is there a gap to the WEST of current cell
            if (maze[curr - 1] == numcells):
                maze[curr - 1] = fval + 1        # set flood value in this cell
                proclist[n] = curr - 1           # save flood cell for future processing
                n = n + 1                        # update processing list number
                if (proclist[n-1] == fin):       # check if finished flooding
                    flooded = 1                  # set flag to stop loop
        #print (proclist[n-1] , fin)
         # print (strt, fin, nxt, n, proclist)
        
        curr = proclist[nxt]             # get the location of the next cell to process
        nxt = nxt + 1                        # point to next item to process on the list
        
        if (nxt > n):    # check if flood unable to continue as no more cells accessible
            floodfail = 1                     # set flood failure status flag
            flooded = 1 # stop  the flooding loop
            if (debug == 1):
                print (strt, fin, nxt, n, proclist)
        #print ("after flood")
        #showflood()
    floodend = time.ticks_ms() # get time now
    floodtime = floodend - floodstart
    if (debug == 1):
        print ("floodtime", floodtime, " cleared", floodcleared )
    return                                    # return 
    
        #print (curr, n, nxt, fval, proclist[n-1])
  
    #showflood()
    #showwalls()
    #halt()    
```

**What you still need to do:**

You still need to traverse through the cells, detecting the walls in each cell and putting the relevant values in the walls array corresponding to the walls seen. Then rerun the floodmaze routine after you find the walls in each cell, to determine in which direction you should go next.
