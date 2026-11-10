---
title: Line Follower logic
date: '2024-07-26T19:02:05Z'
lastmod: '2024-07-26T19:03:40Z'
weight: 1
wp_id: 3210
---

Line follower logic  
The processing circuits and the logic within them are what makes it a line follower. As a minimum it needs to be able to detect whether the line sensors are seeing black or white and turn the line follower left or right. This will be done by speeding up or slowing down the motors on one side if we are using the wheelchair or tank drive layout.  
Here is the some of the logic that we may want to implement – assuming we are following a white line on a black background

  - If both central line sensors are seeing white, keep going straight ahead, as we are right on the line
  - If the left sensor of the central pair is seeing black and the right one is seeing white we need to turn right a bit, as we have drifted slightly to the left of the line
  - If the right sensor of the central pair is seeing black and the left one is seeing white we need to turn left a bit, as we have drifted slightly to the right of the line  
    This will be OK as long as we get back on the line as soon as we start to drift off it, but does not work if we come off the line and so see black with both line sensors, so we might want to add this extra logic for when both central sensors are seeing black:
  - If the last sensor to see the white line was the left one of the central pair, we need to turn left, as we have gone off the line to the right
  - If the last sensor to see the white line was the right one of the central pair, we need to turn right, as we have gone off the line to the left  
    This logic works very well for a fixed speed line follower.  
    However, if we want to be able to stop at the end of the course or go faster on the straights, we also need some extra logic to detect the markers and take account of them accordingly.  
    In standard UK competitions the course start and stop markers are on the right side of the line and the corner markers are on the left side of the line, so we might want to add some logic that says:
  - If the right side sensor sees white for the second time, stop the motors, as we have reached the end of the course
  - If the left side sensor sees white, adjust the speed of the motors between fast and slow, i.e. speed up for the straights and slow down for the corners  
    This is not quite as straightforward as it sounds, as we will see a white marker many times as we cross it, so we only want to make the speed change as we detect a change from black to white (at the start of the marker) or on a change from white to black (at the end of the marker). In addition to this there can be crossings on the course where a white line will go across the track at right angles. If we see this on both sides at the same time, we need to ignore it.
