## Laptop Builder

---

### Download VSCode Live Share

Get it [here](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)

---


### Download Template Code

```bash
# open powershell
cd <your-learning-folder>

git clone https://github.com/mingxiangchan/ts-node-boilerplate

# rename the downloaded folder
Rename-Item ./ts-node-boilerplate <new-folder-name>

cd <new-folder-name>

# install javascript dependencies
npm install
```


---

### Instructions

1. Prompt the user to select the following specs for his laptop:

    - HDD (128GB, 256GB, 512GB)
    - RAM (8GB, 16GB, 32GB)
    - CPU (i3, i5, i7)
    - Screen (1920x1080, 2560x1440, 2560x1440-Touchscreen)

2. Show the user the total price for the selected components

---

### Pseudocode

1. for each category
    - show the user a question: Please select your <something>
    - show the user the possible selections
    - ask them to select one
    - move on to next question
2. at the end
    - show them which components they selected previously
    - show them to total price of all the selected components