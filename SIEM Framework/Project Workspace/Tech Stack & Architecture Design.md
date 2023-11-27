
# Opinionated/Curated Tech Stacks & Architectures
- Solution Group Numbers:
	- 1- ETL Proxy
	- 2- Data Ingestion
	- 3- Data Storage
	- 4- Data Processing
	- 5- Data Analysis
	- 6- Automation
## SIEM Focus
### Open Source
- Graylog
	- 

- Wazuh
	- 
### Proprietary
- Sentinel
	- 

- Hive Project
	- 

- Matano
	- .

- Devo
	- .

- ELK Stack 
	- ELK - Elasticsearch, Logstash, Kibana
	- [ELK stack implementation tips for production : r/elasticsearch](https://www.reddit.com/r/elasticsearch/comments/112wcst/elk_stack_implementation_tips_for_production/) 
	- https://logz.io/blog/open-source-elasticsearch-doubling-down/
		- Logz.io offers a unified cloud observability platform with log management based on Kibana,  Prometheus as a service, distributed tracing based on Jaeger, and cloud SIEM.  The Logz.io team is intimately immersed with both Kibana and Elasticsearch.
## Innovative Tech Stack
### Open Source
- Files to Minio to Trino and Iceberg to Hive Metastore to Maria DB
	- [High-performance open-source Data Lakehouse at home | by Daniel Palma | Medium](https://medium.com/@danthelion/high-performance-open-source-data-lakehouse-at-home-56c8d7fa87b5) 
- 
### Proprietary
- Loki, Grafana
	- 

- Databricks
	- 

- Dremio
	- .
## Ranked Qualitatively
### Qualitative Ranking System
#### Code
JS:
```
const container = document.getElementById('jsoneditor');

const options = {
    mode: 'code',
    modes: ['code', 'form', 'text', 'tree', 'view', 'preview'],
    onModeChange: function (newMode, oldMode) {
        console.log('Mode switched from', oldMode, 'to', newMode);
    }
};

const configureSections = document.getElementById('configureSections');

let sc_editor;
let s_editor;
let numEntities;

document.getElementById('configureEntities').addEventListener('click', () => {
    numEntities = document.getElementById('numEntities').value;
    const entityArray = Array.from({ length: numEntities }, (_, i) => i + 1);
    const entitySchema = {
        type: 'object',
        properties: {},
    };
    entityArray.forEach((entity) => {
        entitySchema.properties[entity] = {
            type: 'object',
            properties: {
                name: { type: 'string' },
                description: { type: 'string' },
                terms: {
                    type: 'array',
                    items: { type: 'string' },
                },
            },
        };
    });

    const entityData = entityArray.reduce((data, entity, index) => {
    data[entity] = {
        name: `Solution_Category_${index + 1}`,
        description: '',
        terms: [],
    };
    return data;
}, {});

    sc_editor = new JSONEditor(document.getElementById('solutionCategoriesEditor'), { ...options, schema: entitySchema}, entityData);
    
    // Show the hidden sections
    configureSections.classList.remove('hidden');

		const solutionsData = {
      1: {
          name: 'solution_1',
          categories: [1, 2],
          value: 5,
      },
      2: {
          name: 'solution_2',
          categories: [2],
          value: 3,
      },
      3: {
          name: 'solution_3',
          categories: [1],
          value: 4,
      },
  	};

    s_editor = new JSONEditor(document.getElementById('solutionsEditor'), { ...options}, solutionsData);

		//console.log(JSON.stringify(sc_editor.get(), null, 2));
		//console.log(JSON.stringify(s_editor.get(), null, 2));
    
});

function calculate_score(entity_values, max_entities, k) {
    // Calculate the sum of entity values
    const sum_of_values = entity_values.reduce((acc, value) => acc + value, 0);
    // Calculate the penalty for entity count
    const penalty = (max_entities - entity_values.length) * k;
    // Calculate the score
    const score = sum_of_values * penalty;
    return score;
}

function combinations(arr, k) {
    const result = [];

    function backtrack(start, current, k) { // Pass k as an argument
        if (current.length === k) {
            result.push(current.slice());
            return;
        }

        for (let i = start; i < arr.length; i++) {
            current.push(arr[i]);
            backtrack(i + 1, current, k); // Pass k to the recursive call
            current.pop();
        }
    }

    backtrack(0, [], k); // Initialize k when calling the function
    return result;
}

document.getElementById('generateTechStacks').addEventListener('click', () => {

    const solution_categories = sc_editor.get(); 
    const solutions = s_editor.get();
		const textBox = document.getElementById("KValue");
		const k = textBox.value;
		const max_entities = numEntities;
    const r = 2; // Set the desired number of solutions in each combination
    const combinationsResult = combinations(Object.keys(solutions), r);
    
  const scored_combinations = [];
  for (const combo of combinationsResult) {
      const entity_values = combo.map((sol) => solutions[sol].value);
      const score = calculate_score(entity_values, max_entities, k);
      scored_combinations.push({ combo, score });
  }

	scored_combinations.sort((a, b) => b.score - a.score);

	const techStacksContainer = document.getElementById('techStacks');

  scored_combinations.forEach((stack, index) => {
      const stackElement = document.createElement('div');
      stackElement.classList.add('tech-stack');

      const scoreElement = document.createElement('div');
      scoreElement.classList.add('score');
      scoreElement.textContent = `Tech Stack ${index + 1} - Total Score: ${stack.score}`;
      stackElement.appendChild(scoreElement);

      const solutionsElement = document.createElement('div');
      stack.combo.forEach((solIndex) => {
          const solution = solutions[solIndex];
          const solutionElement = document.createElement('div');
          solutionElement.classList.add('solution');

          const categories = solution.categories.map((cat) => solution_categories[cat].name);
          const categoryString = categories.join(', '); // Combine the categories

          const solutionName = `${solution.name} (${solIndex}): (${categoryString})`;
          solutionElement.textContent = `${solutionName} - value of ${solution.value}`;
          solutionsElement.appendChild(solutionElement);
      });
      stackElement.appendChild(solutionsElement);

      techStacksContainer.appendChild(stackElement);
  });
		
});
```
HTML:
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Configure Tech Stack</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <script src="jsoneditor.min.js"></script>
    <script src="script.js"></script>
    
    <h1>Tech Stack Options Setup</h1>
      <label for="numEntities">Number of Categories: </label>
      <input type="number" id="numEntities" min="1">
      <button id="configureEntities">Configure Categories</button>
  <div id="configureSections" class="hidden">
    <h2>Configure Solution Categories</h2>
      <div id="solutionCategoriesEditor" class="jsoneditor"></div>
    <h2>Configure Solution Options</h2>
      <div id="solutionsEditor" class="jsoneditor"></div>
    <h1>Tech Stack Generation & Analysis</h1>
      <div>
        <label for="textbox">Tuning Value:</label>
        <input type="text" id="KValue" placeholder="Enter number">
      </div>
      <br>
      <button id="generateTechStacks">Generate Tech Stacks</button>
      <div id="techStacks"></div>
  </div>
</body>
</html>
```
CSS:
```
body {
    font-family: Arial, sans-serif;
}

.tech-stack {
    border: 1px solid #ccc;
    margin: 10px;
    padding: 10px;
    background-color: #f9f9f9;
}

.solution {
    margin: 5px 0;
}

.solution-name {
    font-weight: bold;
}

.category {
    color: #007bff;
}

.score {
    font-size: 1.2em;
    color: green;
}

# Fundamental Security Visibility & Data Engineering
![1000](SIEM_framework_2023)
