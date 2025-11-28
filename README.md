# Global Layoffs SQL Case Study  
---

## 💬 Have You Ever Wondered What MASS Layoffs Really Look Like Behind the Scenes?

Headlines will tell you:

> “Tech company lays off 10,000 employees.”  
> “Finance giant cuts 18% of its workforce.”  
> “Thousands laid off due to economic uncertainty.”

But behind these headlines are even deeper questions:

- **Which industries are actually collapsing the fastest?**  
- **Which countries are hurting the most?**  
- **Are layoffs slowing down — or are we just getting started?**  
- **Which companies laid off more people than entire nations?**  
- **Are certain regions much more unstable than others?**

Therefore, in this project I aimed to answers these questions using real global layoff data, MySQL real-world analysis to uncover the truth behind global layoffs across multiple years and thousands of events.

But before we dive into charts and trends.
let’s remember the human side of this story.
These arent' just numbers... 
**They’re careers, families, dreams, disappointments, and fresh starts.**.
---

# 🎯 Why I Wanted to Analyze Layoffs

Like many others, I watched jobs come and go:

- One week a tech company cuts 12,000 people  
- The next week, startups collapse overnight  
- Departments wiped out completely  
- Hiring freezes everywhere  
- People with 10+ years of experience suddenly out of work  

And I wondered:

> **“Is this normal? Are these just isolated incidents… or part of a bigger global pattern?”**

So I decided to use SQL and a little bit of Tableau visuals to uncover the truth.

I wanted this project to blend:

- My real-world **banking & finance experience**  
- My **SQL-Tableau analysis skills**  
- A dataset large enough to reveal global economic signals  
- And a storytelling approach to sum it all up!

---

# 🔍 What You’re Going to Learn from This Project

By the time you finish this breakdown, you’ll understand:

### ✔️ Which industries suffered the deepest cuts  
### ✔️ Which countries carried the heaviest burden  
### ✔️ Which companies topped yearly layoff rankings  
### ✔️ How layoffs evolved month-by-month  
### ✔️ Which companies almost *collapsed entirely* (80–100% layoffs)  
### ✔️ How global economic stress shows up in workforce data

This is real-world, practical business intelligence to have — not just data results.

---

# 📚 About the Dataset

You can download the file here 👉: - [Raw Data (CSV)](data/Raw_Global_layoffs_file.csv)

The dataset contains **global layoff events** with:

- Company  
- Country  
- Industry  
- Count of employees laid off — Total Laid off
- Percentage of workforce laid off — Percentage Laid Off
- Stage (startup maturity)  
- Funds raised  
- Date of event (messy formats)

*But before analysis, it needed serious cleaning.*

Real data → real mess:

- Duplicate records
- Inconsistent formatting  
- Missing values
- Irregular spacing  
- Blank rows
- Non-standardized fields

So before analysis came **data cleaning**.

---

#  1. DATA CLEANING STAGE 

As any analysis, this dataset required cleaning, easily one of the most crucial parts for reliable insights.

---

## 🩹 Step 1 — Create a Staging Table  
Never touch raw data. Make a safe copy.


![Staging Table Creation](images/first_staging_table.png)

---

## 🗄 Step 2 — Insert Raw Data into the Staging Table


![Staging Table Insert](images/staging_table_insert.png)

---

## 🧹 Step 3 — Detect and Remove Duplicates  
This dataset contained numerous duplicate records, so I used the `ROW_NUMBER()` function to identify them. Next, I created a new staging table, `layoffs_staging2`, to remove the duplicates. This approach bypassed the MySQL limitation that prevents the direct deletion of duplicate rows using CTE, ensuring that only distinct values were retained in the new table.


![Removing Duplicates Query](images/removing_duplicates.png)

Now the data is clean enough for the following sections of Explorotary Data Analysis (EDA).

---

# 🏭 2. Industry-Level Analysis  
**Which industries cut the deepest?**

This is NOT “who laid off the most people”.  
This is **how much of their workforce they eliminated**, on average.

---

## 📊 Average Percentage of Workforce Laid Off by Industry  
  
![Average Percentage Query](images/average_percentage_laid_off_query.png)

## 📊 Results  

| ![Average Percentage Results](images/average_percentage_laid_off_results.png) | ![Count vs Percent layoffs](images/Count%20vs%20Percentage%20Layoffs_Tableau.png) |
|---|---|

---

## 🧠 Insight  
- **Aerospace** → the most severe average layoffs (~29%)  
- **Construction, Crypto, Energy, Food, Travel** → consistently high (19–22%)  
- **Healthcare & Education** surprisingly high  
- **Finance** still averages **~15% per event**

Some industries don’t appear in the press much —  
but their employees quietly faced **deeper cuts**.

---

# 🌍 3. Country-Level Analysis  
**Which countries experienced the highest TOTAL layoffs?**

---

## 🖼 Query  
![Country Totals Query](images/total_laid_off_by_country_query.png)

## 🖼 Results  
![Country Totals Results](images/total_laid_off_by_country_results.png)

---

## 🧠 Insight  
- 🇺🇸 **United States** dominates with **~530k layoffs**  
- 🇮🇳 India → ~61k  
- 🇩🇪 Germany → ~31k  
- 🇬🇧 UK, 🇳🇱 Netherlands, 🇦🇺 Australia, 🇨🇦 Canada, 🇮🇱 Israel also heavily impacted  

The U.S. alone accounts for **60–70% of global layoffs**.

---

# 🩺 4. Country Health Summary  
Totals don’t show patterns — frequency and severity matter too.

---

## 🖼 Query  
![Country Health Query](images/country_health_query.png)

## 🖼 Results  
![Country Health Results](images/country_health_results.png)

---

## 🧠 Insight  
There are **two types of countries**:

### 1️⃣ High-volume cuts (many events, moderate severity)
- United States  
- India  

### 2️⃣ Low-volume but extremely severe cuts
- Singapore (~24% layoffs per event)  
- Israel  
- Australia  
- United Kingdom  

This helps explain economic stability vs. fragility across regions.

---

# 📅 5. Layoffs by Year  
**Which years were the worst?**

---

## 🖼 Query  
![Yearly Totals Query](images/total_laid_off_per_year_query.png)

## 🖼 Results  
![Yearly Totals Results](images/total_laid_off_per_year_results.png)

---

## 🧠 Insight  
- **2023** → Worst year (~264k layoffs)  
- **2022** → Second worst (~164k)  
- **2024** → Still extremely high  
- **2020–2021** → Lower due to early pandemic stimulus  

Confirms a **multi-year correction wave**, not a one-time shock.

---

# 📈 6. Rolling Monthly Totals  
This shows layoffs not as events —  
but as a **growing global wave**.

---

## 🖼 Screenshot  
![Rolling Totals Query + Results](images/rolling_total_month_&_year.png)

---

## 🧠 Insight  
The cumulative number climbs steadily every month.  
Layoffs did **not** slow down — they compounded.

---

# 🏢 7. Top Companies Per Year  
Which companies laid off the most staff in each year?

---

## 🖼 Query  
![Company Ranking Query](images/company_ranking_query.png)

## 🖼 Results  
![Company Ranking Results](images/company_ranking_results.png)

---

## 🧠 Insight  
- **2020** → Uber, Booking.com, Groupon  
- **2021** → Bytedance, Zillow, Katerra  
- **2022** → Meta (11k), Amazon (10k), Cisco  
- **2023–2024** → Tech giants continue dominating  

Each year tells a different economic story.

---

# 💀 8. Collapse-Level Companies (80–98% Layoffs)  
This is the list of companies that nearly **shut down**.

---

## 🖼 Query  
![Collapse Query](images/highest_collapsing_companies_query.png)

## 🖼 Results  
![Collapse Results](images/highest_collapsing_companies_results.png)

---

## 🧠 Insight  
Examples include:

- **Flywheel Sports** — 98%  
- **Pavilion Data** — 96%  
- **NS8** — 95%  
- **Vroom** — 90%  
- **Treehouse** — 90%  
- **OneWeb** — 85%  

These weren’t layoffs.  
These were **full organizational collapses**.

---

# 🧩 9. Main Takeaways

### ✔️ The U.S. is responsible for the majority of global layoffs  
### ✔️ Some industries cut deeper than people realize  
### ✔️ 2022–2023 were the peak years  
### ✔️ Layoffs were a long wave, not a one-time event  
### ✔️ Several companies nearly shut down entirely

This dataset reflects global instability in a way headlines never fully capture.

---

# 🧠 10. Reflections

This project reminded me how much data can reveal about human lives.

Behind each number is:
- A family affected  
- A career disrupted  
- A team dissolved  
- A company struggling to survive  

Using SQL helped transform chaotic raw data into a clear narrative about global economic stress.

This wasn’t just analysis —  
it was a real look into how unpredictable the modern job market has become.

---

# 📁 Repository Structure

