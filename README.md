
# Venom: AI for Traffic Light Control
## Background

Representation:

''0'': green light for direction 1 and hence red light for direction 2;\
''1'': green light for direction 2 and hence red light for direction 1;\
''2'': yellow light for direction 1 and hence red light for direction 2;\
''3'': yellow light for direction 2 and hence red light for direction 1.

__Actions__ representation: (contrary to in paper)

⓪: change state\
①: keep on

## Single Unidirectional Intersection (two roads)

### Model Description:

It is one intersection with only two unidirectional roads, no left or right turning. The number of cars on each road is denoted as ![equ.1](https://latex.codecogs.com/gif.latex?Q_1,&space;Q_2\in&space;I) respectively. The state of the traffic light is denoted by state S, which can be in one of the following four states

* "0": green light for road Q_1, and hence red light for road Q_2;
* "1": red light for road Q_1, and hence green light for road Q_1;
* "2": yellow light for Q_1, and red light for road Q_2;
* "3": red light for road Q_1, and yellow light for road Q_2;

And the transition of states, which is called the action in RL algorithm, can be:

* "0": change;
* "1": keep on;

According to general transportation principles, the state transition of traffic lights could only be unidirectional, which is ![equ.1](https://latex.codecogs.com/gif.latex?"0"\rightarrow{"2"}\rightarrow{"1"}\rightarrow{"3"}\rightarrow{"0"}) under our definition of light states above. The trained RL agent takes the tuple [Q_1, Q_2, S] as input and generates action choice for traffic light.
<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/1inter.png" width="25%">
</p>

### Training:

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/train.png" width="40%">
</p>

## Linear-Network Intersections
### Model Description:

Linear network model is combined with multiple single intersections on a line, as shown in the following graph. Noticing that we don't care much about the outcoming roads, which is denoted by dashed lines.

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/linear_network5.png" width="70%">
</p>

### Visualized Simulation in Experiments: 

the color of lights is 'green' or 'red' or 'yellow'. The black rectangular represents incoming car for periphery of road networks. The numbers indicates number of cars on each road. If the light is 'green', the number of cars in that road will reduce the number of passing cars after transition. If there is 'black rectangular', the number of cars in the corresponding road will increase one after transition. The upper image is the state before transition, while the lower image is the state after transition. 

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/Screenshot.png" width="60%">
</p>

### Training:

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/train1.png" width="40%">
</p>

## Grid-Square-Network Intersections

### Model Description:

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/grid_square_network.png" width="40%">
 </p>

### Visualized Simulation in Experiments: 

  <p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/4*4.png" width="35%">
  </p>

### Training:

 <p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/2*2_100m.png" width="40%">
</p>

## Multi-thread version code for grid network

Apply multi-thread for accelerating training process.

## Agent for single intersection

Single agent for every intersection (instead of single agent for whole road network), input of agent is from each one intersection. All intersections share the same agent, every time agent stores [obs,a,r,obs_] for each intersection, share the same overall reward (`lights.py`) or restore each reward for each intersection (`lights_re.py`).

# Deep Deterministic Policy Gradients

## Background

Basic environments are similar with for DQN, only with main/branch road difference. For all 3 circumstances, main road is direction 2, and branch road is direction 1, larger coming and passing rates on main roads than branch roads. Another difference of DDPG version environment with DQN version is the number of cars on roads (coming, queueing, passing) are more realistic values like 16, 8, etc instead of 0, 1.

## Single Bidirectional Intersection (four roads)

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/ddpg4single.png" width="80%">
</p>

## Linear-Network Intersections

Testing of 10*1 linear network.

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/ddpg4linear.png" width="100%">
</p>

## Grid-Square-Network Intersections

Testing of 10*5 grid network.

<p align="center">
<img src="https://github.com/quantumiracle/DQN_traffic_light_control/blob/master/images/ddpg4grid1.png" width="100%">
</p>
