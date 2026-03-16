# 💼 Freelancer Earnings & Job Trends – Power BI Dashboard

This Power BI project provides a comprehensive analysis of the global freelance job market, covering earnings, platform performance, client behavior, and freelancer success metrics. The dashboard is designed to help job seekers, researchers, and businesses understand compensation patterns and demand trends in the gig economy.

---

## Project Overview

The dashboard provides insights into:

* Earnings distribution across job categories, platforms, and experience levels
* Platform comparison by freelancer count, job completion, and client ratings
* Regional analysis of hourly rates and USD earnings by client location
* Project type breakdown (Fixed vs Hourly) and its effect on earnings
* Marketing spend patterns and their relationship to earnings
* Rehire rate and client satisfaction analysis
* Job success rate distribution and its correlation with earnings
* Job duration trends by experience level and platform
* Payment method preferences by region
* Top 10 freelancer performance ranking based on a custom scoring model

---

## Dashboard Preview

| Cover | Dataset | Dataset 2 |
| --- | --- | --- |
| ![Cover](Dashboard%20Pages/01_Cover.png) | ![Dataset](Dashboard%20Pages/02_Dataset.png) | ![Dataset 2](Dashboard%20Pages/03_Dataset_2.png) |

| Job Category | Platform | Client Rating |
| --- | --- | --- |
| ![Job Category](Dashboard%20Pages/04_Job_Category.png) | ![Platform](Dashboard%20Pages/05_Platform.png) | ![Client Rating](Dashboard%20Pages/06_Client_Rating.png) |

| Project Type | Client Region | Marketing Spend |
| --- | --- | --- |
| ![Project Type](Dashboard%20Pages/07_Project_Type.png) | ![Client Region](Dashboard%20Pages/08_Client_Region.png) | ![Marketing Spend](Dashboard%20Pages/09_Marketing_Spend.png) |

| Rehire Rate | Job Success Rate | Job Duration Days |
| --- | --- | --- |
| ![Rehire Rate](Dashboard%20Pages/10_Rehire_Rate.png) | ![Job Success Rate](Dashboard%20Pages/11_Job_Success_Rate.png) | ![Job Duration](Dashboard%20Pages/12_Job_Duration_Days.png) |

| Payment Method | Best Performance |
| --- | --- |
| ![Payment Method](Dashboard%20Pages/13_Payment_Method.png) | ![Best Performance](Dashboard%20Pages/14_Best_Performance.png) |

---

## Dashboard Structure

The report contains **14 pages** covering all major dimensions of the dataset:

### 📄 Page 1 – Cover
Project title and author introduction.

### 📄 Page 2 & 3 – Dataset
Full dataset preview with column descriptions, sample insights, and potential use cases.

### 📄 Page 4 – Job Category
* Average USD Earnings by Job Category (Bar Chart)
* Completed Average Job by Experience Level and Job Category (Clustered Bar Chart)
* Slicer: Job Category

### 📄 Page 5 – Platform
* Platform Distribution by Job Category (Stacked Bar Chart)
* Platform Distribution (Pie Chart)
* Platform Distribution by Experience Level (Stacked Bar Chart)
* Slicer: Platform

### 📄 Page 6 – Client Rating
* Average USD Earnings by Client Rating (Scatter Chart)
* Average Client Rating by Platform (Bar Chart)
* Average Client Satisfaction (Gauge)
* Average Client Rating by Experience Level (Bar Chart)

### 📄 Page 7 – Project Type
* Project Type Distribution (Pie Chart)
* Platform Distribution by Project Type (100% Stacked Bar)
* Freelancer Distribution by Experience Level and Project Type (Matrix)
* Average USD Earnings by Project Type (Bar Chart)
* Completed Average Job by Project Type (Bar Chart)
* Slicer: Project Type

### 📄 Page 8 – Client Region
* Average USD Earnings and Hourly Rate by Client Region (Map)
* Average Hourly Rate by Client Region (Bar Chart)
* Average USD Earnings by Client Region (Bar Chart)

### 📄 Page 9 – Marketing Spend
* Average Marketing Spend and USD Earnings by Platform (Scatter Chart)
* Average Marketing Spend KPI Card
* Average Marketing Spend by Experience Level (Bar Chart)
* Slicer: Marketing Spend (Range Slider)

### 📄 Page 10 – Rehire Rate
* Average Rehire Rate Distribution by Rating Groups (Line & Clustered Column Chart)
* Average Rehire Rate (Gauge)
* Slicer: Platform (Button Style)

### 📄 Page 11 – Job Success Rate
* Average Job Success Rate (Gauge)
* Job Success Rate Groups (Bar Chart)
* Average Job Success Rate and USD Earnings by Experience Level (Scatter Chart)
* Min / Max Job Success Rate (KPI Cards)
* Slicer: Job Success Rate Filter (Range Slider)

### 📄 Page 12 – Job Duration Days
* Average Job Duration Days by Experience Level (Bar Chart)
* Average Job Duration Days by Project Type (Bar Chart)
* Average Job Duration Days and USD Earnings by Platform (Scatter Chart)
* Slicer: Job Duration Days (Range Slider)

### 📄 Page 13 – Payment Method
* Payment Method Distribution (Donut Chart)
* Average Job Success Rate by Payment Method (Bar Chart)
* Client Region Distribution by Payment Method (100% Stacked Bar)
* Average USD Earnings by Payment Method (Treemap)
* Slicer: Payment Method

### 📄 Page 14 – Best Performance
* Top Freelancer ID (KPI Card)
* Top 10 Freelancers Table (Freelancer ID, Platform, Total Earnings, Avg Success Rate, Avg Rating, Performance Score)
* Performance Formula: `50% Job Success Rate + 30% Earnings USD + 20% Client Rating`

---

## DAX Highlights

**Measures:**

```dax
Average Rating = AVERAGE([Client Rating])
```

```dax
Average Success Rate = AVERAGE([Job Success Rate])
```

```dax
Total Earnings = SUM([Earnings USD])
```

```dax
Freelancer Performance Score = 
VAR NormalizedEarnings = 
    DIVIDE(
        SUM([Earnings USD]), 
        MAXX(ALL(table), [Earnings USD])
    )
VAR NormalizedSuccess = DIVIDE([Average Success Rate], 100)
VAR NormalizedRating  = DIVIDE([Average Rating], 5)
RETURN
    (NormalizedSuccess * 0.50) + (NormalizedEarnings * 0.30) + (NormalizedRating * 0.20)
```

```dax
Top Freelancer ID = 
CALCULATE(
    SELECTEDVALUE([Freelancer ID]),
    TOPN(1, ALL(table), [Freelancer Performance Score], DESC)
)
```

**Groups (Bin type — Size of bins):**

| Group Name | Field | Bin Size | Min | Max |
| --- | --- | --- | --- | --- |
| `Rating Groups` | Client Rating | 0.5 | 3 | 5 |
| `Job Success Rate Groups` | Job Success Rate | 10 | 50.16 | 99.99 |

---

## Filters (Slicers) Used

Interactive slicers are applied on relevant pages:

* **Job Category** – Dropdown (Page 4)
* **Platform** – Dropdown / Button style (Pages 5, 10)
* **Project Type** – Button style (Page 7)
* **Payment Method** – Dropdown (Page 13)
* **Marketing Spend** – Range Slider (Page 9)
* **Job Success Rate** – Range Slider (Page 11)
* **Job Duration Days** – Range Slider (Page 12)

---

## Dataset

**Source:** [Kaggle – Freelancer Earnings and Job Trends](https://www.kaggle.com/datasets/shohinurpervezshohan/freelancer-earnings-and-job-trends)

The dataset contains information about freelancers across multiple platforms and job categories with the following fields:

`Freelancer_ID` · `Job_Category` · `Platform` · `Experience_Level` · `Client_Region` · `Payment_Method` · `Earnings_USD` · `Hourly_Rate` · `Job_Completed` · `Job_Success_Rate` · `Client_Rating` · `Job_Duration_Days` · `Project_Type` · `Rehire_Rate` · `Marketing_Spend`

**Platforms:** Fiverr · Upwork · Toptal · Freelancer · PeoplePerHour  
**Job Categories:** Web Development · App Development · Data Entry · Digital Marketing · Customer Support · Content Writing · Graphic Design · SEO  
**Experience Levels:** Beginner · Intermediate · Expert  
**Client Regions:** Asia · Australia · Canada · Europe · Middle East · UK · USA

---

## 🗃️ File Structure

```
📁 Freelancer_Earnings_Job_Trends
├── 📁 Dashboard Pages
│   ├── 01_Cover.png
│   ├── 02_Dataset.png
│   ├── 03_Dataset_2.png
│   ├── 04_Job_Category.png
│   ├── 05_Platform.png
│   ├── 06_Client_Rating.png
│   ├── 07_Project_Type.png
│   ├── 08_Client_Region.png
│   ├── 09_Marketing_Spend.png
│   ├── 10_Rehire_Rate.png
│   ├── 11_Job_Success_Rate.png
│   ├── 12_Job_Duration_Days.png
│   ├── 13_Payment_Method.png
│   └── 14_Best_Performance.png
├── 📁 Dataset
│   └── freelancer_earnings_job_trends.csv
├── 📁 Power BI
│   └── Freelancer_Earnings_Job_Trends.pbix
└── README.md
```