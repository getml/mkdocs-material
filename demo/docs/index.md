# Showcase


<style>
.md-typeset .panzoom-box {
    background-color: transparent !important;
}
.md-typeset > .panzoom-box,
.md-typeset .panzoom-box_:not(.result .panzoom-box) {
    border: .05rem solid var(--md-code-bg-color);
    border-bottom-left-radius: .1rem;
    border-bottom-right-radius: .1rem;
    border-top-width: .1rem;
}
</style>


## **Abstract Data Model**

```` markdown title="Abstract Data Model"
``` mermaid
flowchart TB
subgraph data_model["<label style="font-size:0.8em;font-weight:bold;opacity:0.55;">data model [type: star schema]</label>"]
  direction TB
  
  population[["<b>population</b>"]]

  expenditures["<b>expenditures</b>"]
  households["<b>households</b>"]
  household_members["<b>household_members</b>"]

  population_join_households("<label style="opacity:.5">on: </label>HOUSEHOLD_ID
  <label style="opacity:.5">relationship: </label>many_to_one")

  population_join_household_members("<label style="opacity:.5">on: </label>HOUSEHOLD_ID
  <label style="opacity:.5">relationship: </label>many_to_one")

  population_join_expenditures("<label style="opacity:.5">on: </label>HOUSEHOLD_ID
  <label style="opacity:.5">time_stamp: </label>TIME_STAMP")

  class population_join_households,population_join_household_members,population_join_expenditures joinClass;
  classDef joinClass stroke-dasharray:3 3,opacity:1,stroke-opacity:0.3,font-size:0.95em;


  households --- population_join_households --> population
  household_members --- population_join_household_members --> population 
  expenditures --- population_join_expenditures --> population
end

style data_model opacity:0.3;
```
````

<div class="result" markdown>

```mermaid
flowchart TB
subgraph data_model["<label style="font-size:0.8em;font-weight:bold;opacity:0.55;">data model [type: star schema]</label>"]
  direction TB
  
  population[["<b>population</b>"]]

  expenditures["<b>expenditures</b>"]
  households["<b>households</b>"]
  household_members["<b>household_members</b>"]

  population_join_households("<label style="opacity:.5">on: </label>HOUSEHOLD_ID
  <label style="opacity:.5">relationship: </label>many_to_one")

  population_join_household_members("<label style="opacity:.5">on: </label>HOUSEHOLD_ID
  <label style="opacity:.5">relationship: </label>many_to_one")

  population_join_expenditures("<label style="opacity:.5">on: </label>HOUSEHOLD_ID
  <label style="opacity:.5">time_stamp: </label>TIME_STAMP")

  class population_join_households,population_join_household_members,population_join_expenditures joinClass;
  classDef joinClass stroke-dasharray:3 3,opacity:1,stroke-opacity:0.3,font-size:0.95em;


  households --- population_join_households --> population
  household_members --- population_join_household_members --> population 
  expenditures --- population_join_expenditures --> population
end

style data_model opacity:0.3;
  
```

</div>





## **Materialized Data Model**

```` markdown title="Abstract Data Model"
``` mermaid
---
title: "Consumer expenditure: getML data model details "
---
%%{init: {
  "themeCSS": [
    "path.er.relationshipLine[marker-end*=ONLY_ONE_END] {marker-end:none;}",
    "path.er.relationshipLine[marker-start*=ONLY_ONE_START] {marker-start:none}",
    "g[id*=join] rect:first-child {stroke_:none;rx:5;opacity:0.4}",
    "g[id*=join] rect:first-child + text {font-size:9px!important;font-weight:bold;text-transform:uppercase;dominant-baseline:central!important;}",
    "g[id*=join] text {opacity:0.8}",
    "g[id*=join] rect:not(:first-child) {stroke:none;fill:none;opacity:.7}",
    "g[id*=join] text[id*=type] {}",
    "g[id*=join] text[id*=name] {display:none;}",
    "marker#ZERO_OR_MORE_START circle {display:none}",
    "marker#ZERO_OR_MORE_END circle {display:none}",
    "marker#ZERO_OR_ONE_START circle {display:none}",
    "marker#ZERO_OR_ONE_END circle {display:none}"
    ]
}}%%
erDiagram
    population }o--|| population_join_households: ""
    population_join_households ||--o| households: ""
    population }o--|| population_join_expenditures: ""
    population }o--|| population_join_household_members: ""
    population_join_expenditures ||--o{ expenditures: ""
    population_join_household_members ||--o{ household_members: ""

    population_join_households["join"] {
        on _ "HOUSEHOLD_ID"
        relationship _ "many_to_one"
    }
    population_join_household_members["join"] {
        on _ "HOUSEHOLD_ID"

    }
    population_join_expenditures["join"] {
        on _ "HOUSEHOLD_ID"
        time_stamp _ "TIME_STAMP"
    }
    expenditures["expenditures"] {
        time_stamp TIME_STAMP
        join_key HOUSEHOLD_ID
        target GIFT
        categorical MONTH
        categorical YEAR
        categorical PRODUCT_CODE "subroles: include.substring"
        numerical COST
        unused_float IS_TRAINING
        unused_string EXPENDITURE_ID
    }
    households["households"] {
        join_key HOUSEHOLD_ID
        numerical YEAR
        numerical INCOME_RANK
        numerical INCOME_RANK_1
        numerical INCOME_RANK_2
        numerical INCOME_RANK_3
        numerical INCOME_RANK_4
        numerical INCOME_RANK_5
        numerical INCOME_RANK_MEAN
        numerical AGE_REF
    }
    household_members["household_members"] {
        join_key HOUSEHOLD_ID
        categorical MARITAL
        categorical SEX
        categorical WORK_STATUS
        numerical YEAR
        numerical AGE
    }
    population["population"] {
        time_stamp TIME_STAMP
        join_key HOUSEHOLD_ID
        target GIFT
        categorical MONTH
        categorical YEAR
        categorical PRODUCT_CODE "subroles: include.substring"
        numerical COST
        unused_float IS_TRAINING
        unused_string EXPENDITURE_ID
    }
```
````

<div class="result" markdown>

``` mermaid
---
title: "Consumer expenditure: getML data model details "
---
%%{init: {
  "themeCSS": [
    "path.er.relationshipLine[marker-end*=ONLY_ONE_END] {marker-end:none;}",
    "path.er.relationshipLine[marker-start*=ONLY_ONE_START] {marker-start:none}",
    "g[id*=join] rect:first-child {stroke_:none;rx:5;opacity:0.4}",
    "g[id*=join] rect:first-child + text {font-size:9px!important;font-weight:bold;text-transform:uppercase;dominant-baseline:central!important;}",
    "g[id*=join] text {opacity:0.8}",
    "g[id*=join] rect:not(:first-child) {stroke:none;fill:none;opacity:.7}",
    "g[id*=join] text[id*=type] {}",
    "g[id*=join] text[id*=name] {display:none;}",
    "marker#ZERO_OR_MORE_START circle {display:none}",
    "marker#ZERO_OR_MORE_END circle {display:none}",
    "marker#ZERO_OR_ONE_START circle {display:none}",
    "marker#ZERO_OR_ONE_END circle {display:none}"
    ]
}}%%
erDiagram
    population }o--|| population_join_households: ""
    population_join_households ||--o| households: ""
    population }o--|| population_join_expenditures: ""
    population }o--|| population_join_household_members: ""
    population_join_expenditures ||--o{ expenditures: ""
    population_join_household_members ||--o{ household_members: ""

    population_join_households["join"] {
        on _ "HOUSEHOLD_ID"
        relationship _ "many_to_one"
    }
    population_join_household_members["join"] {
        on _ "HOUSEHOLD_ID"

    }
    population_join_expenditures["join"] {
        on _ "HOUSEHOLD_ID"
        time_stamp _ "TIME_STAMP"
    }
    expenditures["expenditures"] {
        time_stamp TIME_STAMP
        join_key HOUSEHOLD_ID
        target GIFT
        categorical MONTH
        categorical YEAR
        categorical PRODUCT_CODE "subroles: include.substring"
        numerical COST
        unused_float IS_TRAINING
        unused_string EXPENDITURE_ID
    }
    households["households"] {
        join_key HOUSEHOLD_ID
        numerical YEAR
        numerical INCOME_RANK
        numerical INCOME_RANK_1
        numerical INCOME_RANK_2
        numerical INCOME_RANK_3
        numerical INCOME_RANK_4
        numerical INCOME_RANK_5
        numerical INCOME_RANK_MEAN
        numerical AGE_REF
    }
    household_members["household_members"] {
        join_key HOUSEHOLD_ID
        categorical MARITAL
        categorical SEX
        categorical WORK_STATUS
        numerical YEAR
        numerical AGE
    }
    population["population"] {
        time_stamp TIME_STAMP
        join_key HOUSEHOLD_ID
        target GIFT
        categorical MONTH
        categorical YEAR
        categorical PRODUCT_CODE "subroles: include.substring"
        numerical COST
        unused_float IS_TRAINING
        unused_string EXPENDITURE_ID
    }

```

</div>
