### Building Charts

+++

### Topics

- how to use 3rd party packages
- how to build charts (line, bar, pie)
- how to convert data to form the correct chart

---

### External Libraries

- use code written by other developers
- don't reinvent the wheel
- avoid custom solution for standardized tasks
- ease of maintainance

---

### npm

- Node Package Manager
- enables downloading and using external libraries

+++

### package.json

- a list of all the external libraries in your project
- running <span class="text-blue">npm install (library-name)</span> adds to this list

+++

### npm install

- downloads library source code to the <span class="text-blue">node_modules</span> folder
- cloning a new Javascript project
- another developer changing the project dependencies 

---

### Integrating Charts into Angular

- [chart.js](https://www.chartjs.org/)
- [ng2-charts](https://valor-software.com/ng2-charts)

---

### How to use external packages

- read the [docs](https://valor-software.com/ng2-charts)
- check the <span class="text-gold">General Info -> Usage</span> section
- check the examples
- each example has a <span class="text-gold">Markup</span> and <span class="text-gold">TypeScript</span> section

### Exercise: Laptop Sales

- Clone [this](https://github.com/cmh114933/data-dashboard-example) template repository
- run <span class="text-gold">npm install</span>
- try removing the <span class="text-gold">ng2-charts</span> dependency
- try re-adding the <span class="text-gold">ng2-charts</span> dependency

---
### Exercise

- implement a basic pie chart

```ts
laptop: 50
handphone: 20
tablets: 40
```

+++
### Exercise

- implement a basic line chart

```ts
horizontal: x, y, z
series 1: {x: 10, y: 20, z: 30}
series 2:  {x: 5, y: 30, z: 15}
```

+++

### Exercise


- implement a basic bar chart

```ts
horizontal: a, b, c, d
series 1: {a: 5, b: 15, c: 14, d: 7}
series 2:  {a: 10, b: 12, c: 8, d: 8}
```

---

### Importing Data

- you can import data from a separate file

```ts
import data from '../../multiYearLaptopSales'
```

---

## Basic

+++

### Pie Chart: 

- <span class='text-gold'>laptop Sales By Model</span>
- use <span class='text-gold'>multiYearLaptopSales.js</span>

+++

### Bar Chart

- <span class='text-gold'>total no. of ppl who liked each movie</span>
- use <span class='text-gold'>moviePreferenceStats.js</span>


+++

### Pie Chart

- <span class='text-gold'>total no. of ppl who liked each movie</span>
- use <span class='text-gold'>movieUserPreference.js</span>

---

## Advanced

+++

### Pie Chart

- <span class='text-gold'>total no. of ppl who liked each movie</span>
- use <span class='text-gold'>moviePreferenceComplicated.js</span>

+++

### Bar Chart: 

- <span class='text-gold'>laptop Sales by year by model</span>
- use <span class='text-gold'>multiYearLaptopSales.js</span>
- series: model
- horizontal-axis: year

+++

### Bar Chart: 

- <span class='text-gold'>profit per model per month</span>
- use <span class='text-gold'>multiYearLaptopSales.js</span>
- series: model
- horizontal-axis: month

---

### Assignment

- Start a new Angular Project, add charts to it
- import [this](https://gist.githubusercontent.com/mingxiangchan/e62818b558c28d61c412cd8362a4a200/raw/c1939a60186d4587b182c0d8e2ebcf0dd34e5a35/data.js) data into the project
- you can check [this docs](https://devdocs.io/javascript/global_objects/array) for docs on how to manipulate arrays
- build the following 3 charts

+++

### Importing the data

```ts
import data from '../data'
```

---

### Pie Chart

- number of images per tag

+++

![chart](pie_chart_1.png)

---

### Bar Chart

- number of likes per tag

+++

![chart](bar_chart.png)

---

### Line Chart

- number of images per month

+++

![chart](line_chart.png)


