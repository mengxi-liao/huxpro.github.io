---
layout:     post
title:      "Scrum: A powerful Agile framework"
date:       2018-02-17 12:10:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Project Management
    - Agile
---

> “Let's do scrum”

Scrum is a very useful Agile framework and works very well especially with Ruby on Rails stack. In this post we will give a detail introduction about what scrum is and how to apply Scrum in projects.

## What is Scrum?

First, Scrum is an Agile framework. Agile is a set of principles that teams apply to make softwares efficiently and fun. For more details about Agile, check this WIKI. On the other hand, **Scrum is a framework (or tool sets) that helps teams to manage product development under Agile**. In Scrum, projects move forward via a series of iterations called sprints. Each sprint is typically two to four weeks long.


![](/img/posts/scrum-a-powerful-agile-framework/scrum-1.png)

## The Scrum Roles

There are only 3 roles in Scrum: product owner, scrum master, and the team.

#### Product Owner

The product owner is the project’s key stakeholder and represents users, customers and others in the process. The product owner is often someone from product management or marketing, a key stakeholder or a key user.

#### Scrum Master

The ScrumMaster is responsible for making sure the team is as productive as possible. The ScrumMaster does this by helping the team use the Scrum process, by removing impediments to progress, by protecting the team from outside, and so on.

#### Scrum Team

A typical scrum team has between five and nine people, but Scrum projects can easily scale into the hundreds. However, Scrum can easily be used by one-person teams and often is. This team does not include any of the traditional software engineering roles such as programmer, designer, tester or architect. Everyone on the project works together to complete the set of work they have collectively committed to complete within a sprint. Scrum teams develop a deep form of camaraderie and a feeling that “we’re all in this together.”

## Scrum Processes

Scrum provides processes to help teams apply Agile principles.

![](/img/posts/scrum-a-powerful-agile-framework/scrum-framework.jpg)

#### Sprint

Scrum is moved in iterations, which are called sprints. A sprint is typically 2 to 4 weeks long. At the beginning of a sprint, a sprint planning meeting is held. In the meeting, A set of stories are selected to complete in the new sprint. The goal of each sprint is to complete these deliverables. At the end of each sprint, a sprint review meeting is held to discuss the completion of each story. Another retrospective meeting is also held to discuss what the team has learned from the sprint and how to maintain or improve the productivity in the future sprints.

#### Sprint Planning Meeting

During the sprint planning meeting, the product owner presents the top items on the product backlog to the team. The Scrum team selects the work they can complete during the coming sprint. That work is then moved from the product backlog to a sprint backlog, which is the list of tasks needed to complete the product backlog items the team has committed to complete in the sprint.

#### The Product Backlog

The product backlog is a prioritized to do features list containing every desired feature or change to the product. Note: The term “backlog” can get confusing because it’s used for two different things. To clarify, the product backlog is a list of desired features for the product. The sprint backlog is a list of tasks to be completed in a sprint. The product backlog should be managed by the product owner. It is often the outcome from continuous communication between the product owner and other stakeholders (customers, users, etc).

#### The Sprint Backlog

The sprint backlog is the team’s to do list for the sprint. At the beginning of each sprint, the team should have a sprint meeting to discuss which stories from the product backlog should be put into the sprint backlog of the coming sprint. For each story, the team then define the tasks to complete the story, estimate the tasks, and then put the tasks into the sprint backlog. All the tasks in the backlog of the current sprint are committed to be completed by the end of the sprint. A story is something a team delivers; a task is a bit of work that a person does. Each story will normally require many tasks.

#### The Daily Scrum

Each day during the sprint, a brief meeting called the daily scrum (Also called standup meeting) is conducted. This meeting helps set the context (what I did yesterday and what I will do on the coming day) for each day’s work and helps the team stay on track. All team members are required to attend the daily scrum. Product owners also need to participate in the standup meeting. If the team has done something out of expectation, the product owner should provide feedback as early as possible to make sure that the team is building expected deliverables.

#### Sprint Retrospective

Also at the end of each sprint, the team conducts a sprint retrospective. The goal of the meeting is to learn from the past and discuss how to improve the productivity of the coming sprints. During the meeting, three points are discussed – what the team did well and should continue, what the team should start doing, and what did not work and should stop doing.

## Scrum Artifacts

Scrum provides a set of tools and methods to help teams keep track of progress and team productivity. As more and more sprints a self-organized team runs, the team could use the tools better and know more about their capacity.

#### Story Card

![](/img/posts/scrum-a-powerful-agile-framework/story-card.png)

In scrum, story cards are used to define User stories. Each user story should not only describe the feature, but also tells the developers why we need the feature and who could benefit from the feature. User stories are a good format for product backlog items. The outcome of each user story should be a deliverable. In the sprint backlog, often teams split the selected user story in the current sprint to multiple tasks (design, development, test, deploy, etc).

#### Estimate and Story Points

As we all know, estimate in software project is a hard problem. When the product backlog is being created, the product owner basically is filling the list with different user stories. Some stakeholders may ask how much time will be spent to complete the whole product. A good solution is to ask the team to give a estimate on each user story, then add up the estimate and give a total estimate.

As we all know, estimation in software project is a hard problem. When the product backlog is completed and filled with many user stories. Some stakeholders may ask how much time will be spent to complete the whole product. A good solution is to ask the team to give a estimate on each user story, then add up the estimate and give a total estimate.

In scrum, we use story points to estimate a user story or a task. How to define a point is totally depends on the self-organized team. Story point estimate is a relative comparison. For example, if a team thinks a login screen is a 2, and they think the effort to complete a search feature is 4 times to the login feature, then the search feature is an 8.

Then how to give a time estimate to my boss? Well, it is really hard for a new created team as they do not know their velocity (How many points could be done in each sprint). But as a team completes more and more sprints, the team will know more about the velocity and give more accurate estimate. If the backlog has 300 points, and each sprint the team could complete 20 points in average and each sprint is 2 weeks, the team may respond that the project could be done in 15 sprints, which are 30 weeks in total.

#### Burndown Charts

![](/img/posts/scrum-a-powerful-agile-framework/release-burndown.jpg)

A Burndown chart displays the remaining effort for a given period of time. There are two types of burndown chart.

Sprint Burndown chart is used to keep track of the progress of a sprint. Sprint Burndown shows the relationship between remaining work in the sprint vs the days in the sprint. Work remaining can be shown in whatever unit the team prefers — story points, ideal days, team days and so on. At the beginning of a sprint, a team commits to a number of story points. In each daily screen meeting, the team will update the burndown chart to check if they are ahead or behind schedule.Release Burndown chart is used to keep track of the progress of the whole project. It shows the remaining work in the whole project vs the continuous sprints. It is updated in each sprint meeting. Release burndown chart shows the change of the team velocity of sprints.

Burndown chart is also a good method to reflect scope change. If there is any new requirements added to the scope, the burndown will go up because the story points added. Burndown chart helps product owners and stakeholders to understand how scope change could affect the overall progress of the project.

#### Task Board

When practicing Scrum, we can make the sprint backlog visible by putting it on a Scrum task board. Team members update the task board continuously throughout the sprint; if someone thinks of a new task, she writes a new card and puts it on the wall. Either during or before the daily scrum, estimates are changed (up or down), and cards are moved around the board.

![](/img/posts/scrum-a-powerful-agile-framework/task-board.jpg)

Each row in the task board is a user story in the product backlog. Each story is split to a number of tasks written in task cards and put on the task board. At the beginning of the sprint, all the tasks sit on the to-do column. And each of them will go through each state, from to-do, in progress, to verify, and done, etc. Which column to use depends on the team and the project. Ideally at the end of the sprint, all the cards sit on the done columns.

Many products such as JIRA provides tons of features for Scrum, such as a virtual task board. However, many teams report that a physical task board could help more for better team work. In each daily scrum, team members could move the cards on the board to different status and explain to others what is happening on each task. This could help improving the interaction and collaboration of the whole team.

![](/img/posts/scrum-a-powerful-agile-framework/physical-task-board.png)

## The Scrum Spirit: Inspect & Adapt

Therefore, why do we do development work in these short cycles? To learn. Experience is the best teacher, and the scrum cycle is designed to provide you with multiple opportunities to receive feedback—from customers, from the team, from the market—and to learn from it. What you learn while doing the work in one cycle informs your planning for the next cycle. In scrum, we call this “inspect and adapt”; you might call it “continuous improvement”; either way, it’s a beautiful thing.

## References

1. [Scrum Overview for Agile Software Development](https://www.mountaingoatsoftware.com/agile/scrum/overview).
2. [Scrum Introduction](http://www.agilelearninglabs.com/resources/scrum-introduction).
