---
title: The Scrum Agile Framework
tags:
  - project management
  - agile
  - scrum
  - wip
categories:
  - [project management]
  - [software development]
date: 2018-11-04 15:41:09
---


Scrum is a popular framework for implementing agile. This article is still work in progress and contains notes I collected from various resources about the Scrum framework.

Last updated: 04/11/2018

<!-- more -->



## Type of domains to solve

### Complex domain ###
SCRUM can be usefull here as many things are still not clear and needs to be figured out. As the team needs to learn as the project advances SCRUM is a good way to get feedbacks early and learn more about the challenges as we go
### Complicated domain ###
These are often experts dominated domains like optimazations and performance issues in domain knowledge. Instead of SCRUM it is beter to have good understanding of the problem and consult expert for best practices/solution offered from experience.
### Simple domain ###
Often relates to repeatable tasks. SCUM might be overkill as it is predictable we cna use the waterfall modell or applying best practices to approach these kinds of projects.
### Disorder domain ###
In a disorder domain you have no idea where the specific problems falls into. This is a dangerous domain, it is not whether which porject management methodology to use. Rather it is important to put the problems in specific domains first.
### Chaotic domain ###
It is chaos, there is urgent needed. This is not the right time to SCRUM and making logs etc. Urgency is important, decission needs to be made immediately.
### Interrupt drive domain ###
Quick fixes, support and services tasks falls into this domain. Things that migt or might not need urgency depending on the situation. Better approach might be the Kanban agile approach.

## Sequential vs Agile SCRUM approach
Development is different than production. In production we reproduce the same. In development we make changes and tend to make new things each time. When after development we are happy with what we have we can go into production and reproduce (i.e.  copy and paste).

It is important to understand that one approach is not better then the other one. It all depends on the type of project and domain we are in.
* Plan-drive, sequential development assumes that we will get things right up front and all the different pieces will come together in the effort.
* SCRUM combines iterative and incremental development approaches
	* *Iterative development* - Using multiple pass to improve product. Biggest downside is that in the presence we don’t know how much iteration we need.
	* *Incremental development* - Break product in smaller pieces, learn and adapt. The biggest drawback is that we might lose the big picture. Looking at trees but not the forest.

A scrum team typically consists of around seven people who work together in short, sustainable bursts of activity called sprints, with plenty of time for review and reflection built in. One of the mantras of scrum is “inspect and adapt,” and scrum teams are characterized by an intense focus on continuous improvement—of their process, but also of the product.

## Roles
### Product owner
* Holds the vision for the product
* Represents the interests of the business
* Represents the customers
* Owns the product backlog
* Orders (prioritizes) the items in the product backlog
* Creates acceptance criteria for the backlog items
* Is available to answer team members’ questions

### Scrum master
* Scrum expert and advisor
* Coach
* Impediment bulldozer
* Facilitator

### Team member
* Responsible for completing user stories to incrementally increase the value of the product
* Self-organizes to get all of the necessary work done
* Creates and owns the estimates
* Owns the “ how to do the work” decisions
* Avoids siloed “not my job” thinking

## Artifacts
### The product backlog
The product backlog is the cumulative list of desired deliverables for the product. This includes features, bug fixes, documentation changes, and anything else that might be meaningful and valuable to produce. Preferably ordered by importance.

#### Characteristics of good product logs (DEEP)
* Detailed appropriately - priority and small sized top
* Emergent - constantly updated
* Estimated - effort to develop the item
* Prioritized - prioritize the near-term items destined for following few sprints for optimize flow (too much to vs to little effects on contious flow)

#### Grooming
Grooming refers to three principle activites: creating, refining, estimating and priotizing. While grooming is a collaborative activity, the product owner is the one to make de final decissions. Grooming is a constant process as the project advances more knowledge, feedback and experience will we acquired to adjust the product backlog accordingly.

#### Product backlog size and quantity
General speaking you want one backlog for one product. However for large companies with large products this might not be possible or inefficient. We can split a product backlog hierarchically:
* Portfolio backlog (epics)
* Program backlog (features)
* Team backlog (sprintable stories)

In general, it is recommended to let multiple teams work on differenct product backlogs vs one team working on several product backlogs. In the later case it might be better to merge the product backogs into one back one and prioritize accordingly.

### User stories
User stories for a part can be compared with requirements in sequential planning. However, user stores are more relaxed and flexible as it is totally normal and acceptable that the stories evolve overtime as the team leads more. User stories invite people to discuss and talk bout the topic.

#### Ways to gather stories
* Workshop - Defining the user role -> as a <role> I would like to be able to <action> so that <benefit/value>. Using personas, topdown or bottom up approach.
* Story mapping -  Epic -> themes -> stories, decompose big to small. Prioritize vertically.

#### INVEST in good stories
* Independent
* Negotiable
* Valuable
* Estimatable
* Small

### The spring backlog
The product backlog is the cumulative list of desired deliverables for the product. This includes features, bug fixes, documentation changes, and anything else that might be meaningful and valuable to produce. Includes:
* Stories (deliverables)
	* Tasks

### Burncharts
A burn chart shows us the relationship between time and scope. Time is on the horizontal X-axis and scope is on the vertical Y-axis. A burn up chart shows us how much scope the team has got done over a period of time.

### Task board (Kanban)
The simplest task board consists of three columns: to do, doing and done. Tasks move across the board, providing visibility regarding which tasks are done, which are in progress, and which are yet to be started.

## The sprint cycle (average of 2 weeks)
1. Sprint planning (2hrs)
2. Daily standups (15 mins)
3. Story time (1x per week)
4. Sprint review (30 mins)
5. Retrospective (90 mins)

## Resources:
* [Book] SCRUM: a breathtakingly brief and agile introduction
* [Book] Essential SCRUM: a pratical guide to the most popular agile process
