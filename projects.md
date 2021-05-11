---
layout: page
title: Projects
---

My research at its core is motivated by the vision of continually evolving support
robots that become more self-sufficient by learning from their mistakes and human
supervision. I am very interested in the research questions of "what should a robot
learn given a mistake?" and "how can the agent explain _why_ did it learn what it
learnt?". Naturally, my research endevours have found a home exploring the
inter-dependence between data and structure in a given robotic task domain. I consider
myself a system-oriented researcher, and prefer to ground my questions in real-world
applications and observations. To this end, I have also interned at
[Honda Research Institute-USA](#learning-driving-strategies-from-trajectory-level-demonstrations)
and [Vecna Robotics](#learning-indoor-traffic-trends-using-longitudinal-data) to
understand how robots are expected to work in the real-world. I have also architected
and implemented several robot platforms for application-oriented competitions
([WRC](#assembly-challenge--world-robot-summit-2020), [RoboCup](#robocup-at-home-2017))
and exhibitions ([SelfieBot](#selfiebot-for-uc-san-diego-fund-raiser)) which have served
as necessary experience for understanding the structure in robotics domains.

<!-- A collage of project pictures, real robots and simulation -->

<!-- another paragraph linking research together -->

- [Research In-Progress](#research-in-progress)
  - [Plan Repair in Assembly Domain using Prior Knowledge and Novel Data](#plan-repair-in-assembly-domain-using-prior-knowledge-and-novel-data)
- [Past Research](#past-research)
  - [Guided Learning in Simulation: Minecraft and Gazebo](#guided-learning-in-simulation-minecraft-and-gazebo)
  - [Learning Driving Strategies from Trajectory-level Demonstrations](#learning-driving-strategies-from-trajectory-level-demonstrations)
  - [A Taxonomy for Modes of Human-robot Interaction](#a-taxonomy-for-modes-of-human-robot-interaction)
  - [Learning Indoor Traffic Trends using Longitudinal Data](#learning-indoor-traffic-trends-using-longitudinal-data)
- [Technical Projects](#technical-projects)
  - [Assembly Challenge @ World Robot Summit 2020](#assembly-challenge--world-robot-summit-2020)
  - [RoboCup At Home 2017](#robocup-at-home-2017)
  - [SelfieBot for UC San Diego Fund Raiser](#selfiebot-for-uc-san-diego-fund-raiser)

## Research In-Progress

### Plan Repair in Assembly Domain using Prior Knowledge and Novel Data

Given a prior task model and demonstration of its execution, how may a manipulator robot
monitors its progress, catch failures in novel conditions and localize reasons for
failure in semi-structured conditions? Our research is trying to answer this question by
applying meta-reasoning framework on the assembly domain. Given a discrete space of
positions and orientations there are countably finite configurations possible between
two objects however a large portion of this state-space is infeasible and irrelevant to
the task's success, specially in semi-structured environments. Rather than learning a
value-function on this entire space meta-reasoning asks the question: given my previous
experiences and current progress which state and related sub-task have the highest
probability of triggering this failure? By answering this question we may guide a robot
learner for more efficient learning by either restricting the state-space or injecting
shaped rewards.

<!-- #### Examples of Task Failures -->

<!-- GIFs of task failures -->

[comment]: # [more...]({% link learning_assembly_prior_knowledge.md%})

## Past Research

### Guided Learning in Simulation: Minecraft and Gazebo

Our pilot study which builds the base for my subsequent thesis research. We wanted to
study if action-plans for given tasks can be grounded in observational descriptions of
the world rather than semantic-only descriptions. We used the world of Minecraft for our
simulated experiment so that actions are deterministic but we used a LIDAR-like sensor
on the agent to observe the world and use occupancy grid as a descriptor. Our research
question was: given a task model and its execution under nominal conditions (grounded in
observations and symbolic descriptors) can the agent learn a variation of that plan in a
slightly different environment (semi-structuredness)? We also present our results on a
simulated manipulator in Gazebo.

<img src="{{site.url}}/resources/minecraft_description.png" width="80%">

[comment]: # [read more...]({{site.url}}/minecraft-gazebo/)

### Learning Driving Strategies from Trajectory-level Demonstrations

HRI-US was interested in exploring how do drivers usually account for partially or
completely occluded pedestrians behind parked vehicles in suburban settings. I modelled
this as a learning from demonstration (keyframes in this instance) problem to (1) train
a trajectory-level constraint-generator using smooth splines, and (2) to study the
effect of size of the parked vehicle and proximity of the parked vechicle to road median
on the characteristics of the possible trajectory-space as compared to usual driving
behavior. To conduct the data collection, analysis and training I implemented a driving
simulator on top of Gazebo using its C++ API for this project. We observed that humans
are much more flexible at following "do not cross the yellow line" rule under certain
contexts, and were able to learn these trends as constraints using
keyframe-representation of driving demonstrations. We used the learned trajectories as
constraints on the possible valid trajectories which would then be consumed by
trajectory-planner of the vehicle. HRI-US subsequently patented this component as:
_Keyframe-based Autonomous Vehcicle Operation_.

<figure>
  <img src="{{site.url}}/resources/lfk_hri.png" class="center-img">
  <figcaption><em>(top) Depiction of occluded pedestrian situation in simulation, parked
  vehicles were varied in size as well as distance from road median to analyze effect on
  driving trends, (bottom) Using a case-based approach a complex situation can be
  represented as a linear combination of simple cases, the figures depict generalization
  of approach to novel scenarios</em></figcaption>
</figure>

### A Taxonomy for Modes of Human-robot Interaction

We wanted to identify the key features which affect the nature of interaction between
humans and machines in heterogeneous, goal-oriented teams. Based on an exhaustive review
of past literature we designed a taxonomy for characterizing these interactions and
connecting the past taxonomies with each other based on an upper ontology
classification. We identified three main components characterizing the structure of an
interaction (environment, task, and team), and structure them over two levels:
contextual factors and factors driven by local dynamics. We also present an analysis of
how these factors affect decisions about levels of robot automation and level of
information abstraction in an interaction, and discuss curent gaps in the literature
that can motivate future research. Following is the visual schema for proposed taxonomy:

![Taxonomy for HRI]({{site.url}}/resources/taxonomy.png)

### Learning Indoor Traffic Trends using Longitudinal Data

This project was a collaboration between Dr. Simmons' lab and Vecna Robotics. We wanted
to study if routine trends in human traffic (think going from class to class, moving to
cafeteria during lunch hour or after last class) affect the travel time of an indoor
carrier robot, and if they do can we model and predict these trends based on observable
features. An indoor environment is represented by a topological map, so for each edge in
that map we modelled the travel time as a random variable and used longitudinal data
(>12months) to identify: (a) complex edges which had more than 1 mode of travel-time,
(b) features most relevant at discriminating between these modes. Using this knowledge
we trained a random forest based regressor to predict the travel time given time of day,
day of week, week of year, etc. We observed that our correlated predictor performed
significantly better than an uncorrelated predictor trained on the same data. This
prediction can now be used with a path-planner to optimize over time rather than
distance of map edges.

<div class="row">
  <div class="column">
    <img src="{{site.url}}/resources/modes_of_edges.png" width="100%">
    <em>Real data showing multiple modes of traffic and affected travel time for indoor
    mobile robot</em>
  </div>
  <div class="column">
    <img src="{{site.url}}/resources/regression_result.png" width="100%">
    <em>Result comparing correlated predictor with uncorrelated predictor</em>
  </div>
</div>

## Technical Projects

### Assembly Challenge @ World Robot Summit 2020

One of the more ambitious projects where I led, and managed, a team of 2-3 Masters and
Ph.D. students to architect, model, and implement a dual-arm, autonomous manufacturing
system in ~14 months. I was responsible for modeling the planning domain, implementing
the high-level planner, designing the ROS-based system architecture, liasing with our
sponsors and day-to-day operations. We implemented an end-to-end system for the task
outlined in WRC's rulebook. The WRC task tested a system for: accurate perception,
accurate manipulation and aligning of parts, and efficient execution of insertion
assembly with very tight threshold amongst others. Our system cleared the preliminary
test stage and was chosen as one of the 16 teams to make it to final round.

<figure>
  <video width="640" height="420" controls class="center-img">
    <source src="{{site.url}}/resources/videos/8_x_speed_dual_assembly.mp4" type="video/mp4">
  </video>
  <figcaption><em>Video showing dual-arm execution of a complex three-part assembly
  (click to play)</em></figcaption>
</figure>

### RoboCup At Home 2017

We designed and implemented a speech activated system to assist a human and compete at
RoboCup @ Home Challenge in Nagoya, 2017. The effort was undertaken by a team of 5 Ph.D.
students where I was responsible for implementing person detection and following. We
used [ROS smach](http://wiki.ros.org/smach) to model the high-level decision making and
implemented interfaces to and from planners and perception components. The speech engine
was implemented using Google voice-to-text and an omni-directional speaker. Our team
passed the preliminary screening to be awarded a Human-Support Robot by Toyota and
represent UC San Diego at the competition.
[press release](https://ucsdnews.ucsd.edu/pressrelease/uc_san_diego_takes_part_in_robocup_competition_for_the_first_time)

<figure>
  <video width="640" height="420" controls class="center-img">
    <source src="{{site.url}}/resources/videos/robocup2017_compressed.mp4" type="video/mp4">
  </video>
  <figcaption><em>Our "audition" video to RoboCup Organizers (click to play and turn up
  audio)</em></figcaption>
</figure>

### SelfieBot for UC San Diego Fund Raiser

A fun project we did for UC San Diego fun-raiser which also served as the jumping-board
for the RoboCup @ Home qualification. Using an FSM and Google voice-to-text we created a
selfie taking robot which would click a picture of itself with the visitors and email it
to them. Following video shows the project lead Dr. Shengye Wang taking a selfie with
the robot:

<video width="640" height="420" controls class="center-img">
  <source src="{{site.url}}/resources/videos/fetch_selfiebot.mp4" type="video/mp4">
</video>
