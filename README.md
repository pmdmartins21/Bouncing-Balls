# Boucing balls


This project was created with the intent of simulating balls being thrown in a specific direction and speed and follow a projectile-like trajectory, reflecting the effects of gravity as well as the resistance from walls/floor.


## Requirements
The requirements were the following:
	+ Have a white background Html page
	+ Upon a click on the page, a ball is created with a random color and variable size between 50-100px.
	+ Once created, the ball is thrown with a random speed and direction.
	+ The balls must describe a movement similar to a projectile. This means that direction and speed are affected by gravity force.
	+ Every time the ball hits one of the page limits, the speed decreases by 10% and the direction is inverted.
	+ The top/bottom limits only influences speed in the Y axis
	+ The left/right limits only influences speed in the X axis

## Assumptions
The values for variables like gravity and time were selected to try to simulate as accurately as possible reality.
	+For this project we will use gravity as a positive value to reflect the DOM height reference, as it starts on 0px at top and increases going down.
In order to calculate the movement for the ball, a few options could reflect the physics side of it:
When we're given a direction and speed, that is enough to calculate a velocity vector (Vo) that includes both of these aspects.
This velocity vector can be divided in two, Vx and Vy, which stand for the x and y velocity, and determine the change in movement over time.


For any given ball, we have an initial 
Position: {PosX, PosY}

The initial velocity could be represented as 
v: {vx, vy}

The change in the position over time t, for x and y axis would be as follow:
PosXend = PosXinitial + vx*t
PosYend = PosYinitial + vy*t

The instructions regarding vx were clear that it would be constant, unless upon hitting a wall, where it would be reduced by 10%.
Regarding vy, it must reflect the effects of gravity over time.
FOr the PosY movement we just need the prior PosY, and the vector vy for that given moment, which can be calculated by using the previous vector and adjusting for gravity:

v = vo -gt (or in our project v = vo + gt)
With this value we can calculate the movement on the Y-axis as the initial value + the velocity vector vy:
PosY = PosYi + vt

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```


### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
