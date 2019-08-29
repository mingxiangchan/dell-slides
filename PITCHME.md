### Collaborating with Git

+++

### Topics

- what is git
- why do we use git
- how do we use git

---

### Links

- [Visualizing Git](https://git-school.github.io/visualizing-git/)
- [VSCode Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)

---

#### So Far

1. git clone
2. git commit
3. git push

---

#### Git Branching

+++

- `git branch <branch-name>`
- `git checkout <branch-name>`
- `git merge <branch-name>`

+++

`HEAD`

- represents current position

+++

`git branch <branch-name>`

- creates a branch at the current HEAD

+++

`git checkout <branch-name>`

- moves current HEAD to the last commit for the specified branch

+++

`git merge <branch-name>`

- merge all commits from branch to current HEAD

---

### Exercises

+++

![commit-1](./exercise-1.png)

+++

![commit-2](./exercise-2.png)

+++

![commit-3](./exercise-3.png)

---

### Exercise

+++

### Instructions

1. Create a new folder
2. add a new file <span class="text-gold">message.txt</span>
3. edit its contents with some message
4. run <span class="text-blue">Git: Initialize</span> via <span class="text-blue">Ctrl Shift P</span>
5. run <span class="text-blue">Git: Commit All</span> via <span class="text-blue">Ctrl Shift P</span>

+++

### Branch Creation

1. in terminal, run <span class="text-blue">git checkout -b <branch-name></span>
2. via <span class="text-blue">Ctrl Shift P</span> -> <span class="text-blue">Git: Create Branch</span>
3. in VSCode, lower left corner indicates current branch

+++

### Instructions

1. Create 3 branchs, <span class="text-blue">x</span>, <span class="text-blue">y</span>, <span class="text-blue">z</span>
2. add 2 commits on <span class="text-blue">x</span>
3. add 3 commits on <span class="text-blue">y</span>
4. add 1 commit on <span class="text-blue">z</span>
5. merge <span class="text-blue">x</span> into <span class="text-blue">master</span>
6. merge <span class="text-blue">y</span> into <span class="text-blue">master</span>
7. merge <span class="text-blue">z</span> into <span class="text-blue">master</span>

---

#### Git Remotes

+++

- `git clone <url>`
- `git push origin <branch>`
- `git fetch origin <branch>`
- `git pull origin <branch>`
- `git checkout --track origin/<branch-name>`

+++

### Exercise

- create a repo on github
- run the <span class="text-blue">git remote add origin your-url</span> in terminal
- push branches <span class="text-blue">master</span>, <span class="text-blue">x</span>, <span class="text-blue">y</span>, <span class="text-blue">z</span> to github

+++

### Instructions

- delete your folder
- git clone it
- pull each branch from origin

---

### Assignment

+++

### Create an angular app

- similar to [this](https://coinmarketcap.com/)
- have a [homepage](https://coinmarketcap.com/) displaying a list of items
- have a [page](https://coinmarketcap.com/currencies/bitcoin/) displaying stats for a specific item
- don't need to replicate everything(e.g. nested tabs)

+++

### Requirements

- use Bootstrap to do the styling
- use 1 branch per page
- merging should happen via pull requests
- at least 2 commits per branch
- at least 1 chart 
- at least 1 table per page

+++

### Tips

- just hardcode the data
- don't replicate everything
- main goal is bootstrap + git and angular recap




