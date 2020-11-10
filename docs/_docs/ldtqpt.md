---
#layout: article
title: 雷达图和气泡图
date: 2020-07-27
mermaid: true
chart: true
permalink: /docs/ldtqpt
key: docs-ldtqpt
--- 

## 使用前提

想要在Markdown中使用各种图表，请在文章头部加入以下内容
{:.warning}
  
```
---
chart: true
---
```

## 使用教程  
各项图标的教程，已经在[此处](https://www.chartjs.org/docs/latest/charts/)查看  
下面只是示例与展示  
  
## 雷达图

```chart
{
  "type": "radar",
  "data": {
    "labels": [
      "Eating",
      "Drinking",
      "Sleeping",
      "Designing",
      "Coding",
      "Cycling",
      "Running"
    ],
    "datasets": [
      {
        "label": "My First dataset",
        "backgroundColor": "rgba(179,181,198,0.2)",
        "borderColor": "rgba(179,181,198,1)",
        "pointBackgroundColor": "rgba(179,181,198,1)",
        "pointBorderColor": "#fff",
        "pointHoverBackgroundColor": "#fff",
        "pointHoverBorderColor": "rgba(179,181,198,1)",
        "data": [
          65,
          59,
          90,
          81,
          56,
          55,
          40
        ]
      },
      {
        "label": "My Second dataset",
        "backgroundColor": "rgba(255,99,132,0.2)",
        "borderColor": "rgba(255,99,132,1)",
        "pointBackgroundColor": "rgba(255,99,132,1)",
        "pointBorderColor": "#fff",
        "pointHoverBackgroundColor": "#fff",
        "pointHoverBorderColor": "rgba(255,99,132,1)",
        "data": [
          28,
          48,
          40,
          19,
          96,
          27,
          100
        ]
      }
    ]
  },
  "options": {}
}
```

**markdown语法:**

    ```chart
    {
      "type": "radar",
      "data": {
        "labels": [
          "Eating",
          "Drinking",
          "Sleeping",
          "Designing",
          "Coding",
          "Cycling",
          "Running"
        ],
        "datasets": [
          {
            "label": "My First dataset",
            "backgroundColor": "rgba(179,181,198,0.2)",
            "borderColor": "rgba(179,181,198,1)",
            "pointBackgroundColor": "rgba(179,181,198,1)",
            "pointBorderColor": "#fff",
            "pointHoverBackgroundColor": "#fff",
            "pointHoverBorderColor": "rgba(179,181,198,1)",
            "data": [
              65,
              59,
              90,
              81,
              56,
              55,
              40
            ]
          },
          {
            "label": "My Second dataset",
            "backgroundColor": "rgba(255,99,132,0.2)",
            "borderColor": "rgba(255,99,132,1)",
            "pointBackgroundColor": "rgba(255,99,132,1)",
            "pointBorderColor": "#fff",
            "pointHoverBackgroundColor": "#fff",
            "pointHoverBorderColor": "rgba(255,99,132,1)",
            "data": [
              28,
              48,
              40,
              19,
              96,
              27,
              100
            ]
          }
        ]
      },
      "options": {}
    }
    ```
    
## 气泡图

```chart
{
  "type": "bubble",
  "data": {
    "datasets": [
      {
        "label": "First Dataset",
        "data": [
          {
            "x": 20,
            "y": 30,
            "r": 15
          },
          {
            "x": 40,
            "y": 10,
            "r": 10
          }
        ],
        "backgroundColor": "#FF6384",
        "hoverBackgroundColor": "#FF6384"
      }
    ]
  },
  "options": {}
}
```

**markdown语法:**

    ```chart
    {
      "type": "bubble",
      "data": {
        "datasets": [
          {
            "label": "First Dataset",
            "data": [
              {
                "x": 20,
                "y": 30,
                "r": 15
              },
              {
                "x": 40,
                "y": 10,
                "r": 10
              }
            ],
            "backgroundColor": "#FF6384",
            "hoverBackgroundColor": "#FF6384"
          }
        ]
      },
      "options": {}
    }
    ```
