# 📉 Global Layoffs: A Deep Dive Into the Mass Job Cuts of 2020–2023  
### A Full SQL + Data Cleaning + Data Storytelling Case Study  
*By TJ – Data Analyst / Banking & Finance Background*

---

## 💬 Have You Ever Wondered What MASS Layoffs Really Look Like Behind the Scenes?

Headlines will tell you:

> “Tech company lays off 10,000 employees.”  
> “Finance giant cuts 18% of its workforce.”  
> “Thousands laid off due to market downturn.”

But behind those headlines are deeper questions:

- **Which industries are actually hurting the most?**  
- **Which countries are taking the biggest hits?**  
- **Are layoffs accelerating or calming down?**  
- **Which companies lay off more people than entire nations?**  
- **And is this the end… or the beginning of something bigger?**

This project answers all of that using **MySQL**, **data cleaning**, **window functions**, and **storytelling** — but more importantly, through the eyes of someone who has **worked inside the banking and finance system** and seen firsthand how employment cycles shape real human lives.

This isn’t just data.  
This is a **global story of struggle, survival, and economic turbulence** reflected through numbers.

So sit back, relax, grab your popcorn 🍿 —  
and let me show you what I found inside this dataset.

---

# 🎯 Why I Wanted to Analyze Layoffs

For the past several years, I’ve watched layoffs shake industries across the world — especially during and after the pandemic.

I saw:
- Friends lose jobs in tech  
- Entire departments dissolve in finance  
- Companies restructure again and again  
- Job applicants panic as hiring froze overnight  
- Teams going from 20 people to 6

And I wondered:

> **“Is this normal? Or are we living in a once-in-a-generation employment crisis?”**

That curiosity led me to build this project.

I wanted to combine:
- My **banking & finance experience**
- My evolving **SQL & Data Analyst skills**
- And a real dataset that reflects global economic change

This project became a journey — part analytical, part emotional, part investigative.

---

# 🔍 What You’re Going to Learn from This Project

By reading this article, you will learn:

### ✔️ How to clean a messy global dataset using SQL  
### ✔️ How window functions & CTEs unlock deep insights  
### ✔️ Which industries are collapsing the fastest  
### ✔️ Why the U.S. dominates layoff counts  
### ✔️ How layoffs have evolved month-by-month  
### ✔️ And how some companies laid off more people than entire countries

Plus—  
you’ll gain a deeper understanding of the **human impact** behind these numbers.

---

# 📚 Dataset Details

The dataset contains:

- Company  
- Industry  
- Country  
- Total laid off  
- Percentage laid off  
- Company stage  
- Funds raised  
- Date (messy format)  

Over **10,000 rows** representing global layoffs.

But the data was messy:
- Duplicates everywhere  
- Dates in text format  
- Inconsistent company name spacing  
- Meaningless rows  
- Missing values  

Just like a real analyst job.

---

# 🛠️ 1. DATA CLEANING (THE HARD PART)

This dataset needed surgery.

---

## 🩹 Step 1 — Create a staging table

We never touch raw data.  
We protect it like an artifact.

```sql
CREATE TABLE layoffs_staging LIKE raw_world_layoffs_csv;
INSERT INTO layoffs_staging SELECT * FROM raw_world_layoffs_csv;
