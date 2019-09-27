---
marp: true
---

# Software Development Project

---

### Goal

- proper git flow
- proper project management
- design the solution yourselves

---

### The Problem: 

- HR wants to automate exporting internal jobs to other job portals
-  Jobs should initially be created on https://jobs.dell.com
- Should be able to automatically sync to external sites:
    - Job Street
    - LinkedIn
    - Jobs DB
- Any updates will be in sync, e.g. updating and deleting

---

### Project Planning

- use [Pivotal Tracker](https://www.pivotaltracker.com/dashboard)
- write a list of all the features you will need
- write a doc about what technologies you will use and why you use it

---

### Sample: Pomodoro App

- A pomodoro is a block of time (usually 30 mins) where you assign yourself to fully focus on a task
- At the end of the pomodoro should take a 5 min break
- app allows you to:
    - start new pomodoro
    - end it before default end time
    - view previous pomodoros (daily and weekly)

---

## Sample: Pomodoro App

- Frontend
    - **Purpose**
        - show create pomodoro form
        - show current timer, end button
        - show daily view, show tasks worked 
        - show weekly view, chart of pomodoro times across the week
    - **Tech**: Angular, ng2-charts
    - **Deployment**: Netlify

---

## Sample: Pomodoro App

- Backend
    - **Purpose**
        - store pomodoro data
    - **Tech**: Spring, Hibernate, Postgresql
    - **Deployment**: Cloud Foundry
- Scripting: 
    - **Purpose**
        - import pomodoro data from a CSV
        - export pomodoro data to a CSV
    - **Tech**: Python, SQLAlchemy
    - **Deployment**: None

---

## User Stories

- each story should follow the `user does something` format
- discuss with your group members, how many points to assign to a task
- if more than 3 points, split into new card
- attach any diagrams/wireframes to the cards

---

## Shared Tasks 

- need to be discussed among the entire team (regardless of front/backend)
    1. UX Flow and Wireframes
        - E.g. draw.io, Photoshop, Illustrator
    2. DB structure
        - dbdiagram.io
    3. API endpoints
        - Swagger, Postman, stoplight.io, apiary.io
- for now, keep all documentation in pivotal and stoplight.io

---

## Git Flow

- create a repository (possibly multiple)
- add collaborators
- create a `develop` branch
- all branches should be merged to `develop`
- branches should be prepended with `feature`, `hotfix`, `release`, etc. 
    - e.g. `feature/11-user-login`
- **Pivotal Specific**: include the pivotal story ID in the branch name
    - e.g. ID is 11, hence `feature/11-user-login` 

---

## Release flow

- a release contains a set of completed features
- create a `release/<version-number>` branch
- no new features can be added after this
- only fixes are allowed on the release branch
- merge `release/<version-number>` into master when all ready

---

## Exercise

- Write documentation on what kinds of integration you will need for each external job listings site
- documentation should be in API format
- the endpoints you need most likely do not exist, the purpose of documenting this is to send to them and request for these endpoints

