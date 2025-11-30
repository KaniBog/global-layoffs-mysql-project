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

Therefore, in this project I aimed to answers these questions using real global layoffs data, along with MySQL real-world analysis to uncover the truth behind global layoffs across multiple years and thousands of events.

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

# What Readers gain from This Project

By the time you finish reading, you’ll understand:

### ✔️ Which industries suffered the deepest cuts  
### ✔️ Which countries carried the heaviest burden  
### ✔️ Which companies topped yearly layoff rankings  
### ✔️ How layoffs evolved month-by-month  
### ✔️ Which companies almost *collapsed entirely* (80–100% layoffs)  
### ✔️ How global economic stress shows up in workforce data

This is real-world, practical business intelligence — not just data results.

---

# 📚 About the Dataset

You can download the file here 👉 [Raw Data (CSV)](data/Raw_Global_layoffs_file.csv)

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

#  1. Data Cleaning Phase

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

Now the data is clean enough for the following sections of Exploratory Data Analysis (EDA).

---

# 🏭 2. Industry-level Layoff Severity — Two Ways of Measuring the Same Story
---
To understand **which industries cut the deepest?**, I looked at layoffs in two different ways. 

## First Way: Average % of Workforce Laid Off (Company-level Severity)
  
![Average Percentage Query](images/average_percentage_laid_off_query.png)
![Average Percentage Results](images/average_percentage_laid_off_results.png) 
---
This metric shows how aggressively companies within each industry cut their staff. 
- **Aerospace** → the most severe average layoffs (~29%)  
- **Construction, Crypto, Energy, Food, Travel** → consistently high (19–22%)  
- **Healthcare & Education** surprisingly high  
- **Finance** still averages **~15% per event**

*Key Takeaway:* Industries like **Aerospace, Crypto, Travel, and Construction** have extremely high average percentage cuts because many companies inside them executed deep, structural layoffs. 

Revealing how intense layoffs were at the company level.

---
## Second Way: Weighted Industry Layoff % (Industry-Wide Severity)

![Count vs Percent layoffs](images/Count%20vs%20Percentage%20Layoffs_Tableau.png) 


In this `Tableau` representation, I used Tableau’s calculated field interface to build a weighted percentage metric that adjusts for company size and reflects how much of each entire industry’s workforce was actually affected. The dataset includes company-level percentages (for example, one company might lay off 40% while another lays off 100%), but simply averaging these values can distort the true picture.

Instead, I created a calculated field that weights each layoff event by the number of employees affected. This ensures that large-scale layoffs influence the results proportionally, while small startup collapses don’t overwhelm the analysis. The weighted metric provides a far more accurate representation of how deeply each industry was impacted overall, offering a much clearer sense of where the **deepest structural damage** occurred across the global economy.

For example:

- Crypto companies show many 80–100% layoffs (because small startups failed),
BUT the weighted impact is only ~26%,
meaning one out of four crypto jobs disappeared industry-wide.

- Large industries like Tech or Retail show lower weighted percentages
but extremely high total layoffs — meaning layoffs were widespread but distributed.

To wrap up, this metric reveals how deeply layoffs cut into the entire industry’s workforce, not just individual companies.

---

# 🌍 3. Country-Level Analysis  
**Which countries experienced the highest TOTAL layoffs?**

---
![Country Totals Query](images/total_laid_off_by_country_query.png)
![Country Totals Results](images/total_laid_off_by_country_results.png)

---

## Layoffs by Country (Deeper Breakdown)

- 🇺🇸 United States dominates with ~530,000 layoffs, far exceeding every other country in the dataset.
The U.S. alone represents 60–70% of all global layoffs, driven primarily by large tech firms, venture-funded companies, and corporate restructurings after years of rapid expansion.
- 🇮🇳 India follows with ~61,000 layoffs, reflecting the scale of its tech outsourcing sector and hiring freezes post-pandemic.
- 🇩🇪 Germany (≈31k) and 🇬🇧 United Kingdom (≈29k) show significant cuts, mostly tied to financial services, auto manufacturing, and European recession pressures.
- 🇳🇱 Netherlands, 🇦🇺 Australia, 🇨🇦 Canada, and 🇮🇱 Israel also experienced notable workforce reductions, especially in tech, fintech, and high-growth startups.
---
🔍 What These Numbers Actually Suggest
The outsized U.S. layoffs aren’t just a reflection of company count—they’re a reflection of risk appetite and business model:
- The U.S. has more tech giants and high-growth startups than any other country.
- These companies scaled aggressively during 2020–2021, then rapidly downsized when macroeconomic conditions shifted.
- The “hire fast → fire fast” cycle is structurally more common in the U.S. labor market compared to Europe or Asia.

Meanwhile:
- India’s layoff concentration mirrors its large IT and BPO workforce.
- Germany’s cuts align with supply chain disruptions and declines in manufacturing output.
- Israel and Canada both show layoffs tied to venture-capital–funded tech firms tightening spending.
---

🌍 Bigger Picture

Layoffs aren’t evenly distributed—they cluster where tech innovation, venture capital, and rapid scaling occur.
This means the countries with the most layoffs are also the ones with the highest density of:
- tech startups
- cloud/software companies
- aggressive hiring during COVID
- high-paid knowledge workers
- companies dependent on investor confidence
  
Which all correlate with larger and more visible workforce reductions once growth slows.
---
🧠 Key Takeaway

The U.S. dominating layoffs does not necessarily mean its economy is the weakest—it often reflects:
- bigger tech sector
- faster scaling
- more aggressive restructuring
- more companies reporting layoffs publicly
  
In contrast, layoffs in Europe and Asia tend to be smaller, slower, and more regulated, which keeps their numbers far below U.S. levels even during downturns.

---

# 🩺 4. Country Health Summary  
Totals don’t show patterns — frequency and severity matter too.

---
![Country Health Query](images/country_health_query.png)  
![Country Health Results](images/country_health_results.png)

---
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
![Yearly Totals Query](images/total_laid_off_per_year_query.png)
![Yearly Totals Results](images/total_laid_off_per_year_results.png)

---
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
![Rolling Totals Query + Results](images/rolling_total_month_&_year.png)

---
The cumulative number climbs steadily every month.  
Layoffs did **not** slow down — they compounded.

---

# 🏢 7. Top Companies Per Year  
Which companies laid off the most staff in each year?

---
![Company Ranking Query](images/company_ranking_query.png)
![Company Ranking Results](images/company_ranking_results.png)

---
- **2020** → Uber, Booking.com, Groupon  
- **2021** → Bytedance, Zillow, Katerra  
- **2022** → Meta (11k), Amazon (10k), Cisco  
- **2023–2024** → Tech giants continue dominating  

Each year tells a different economic story.

---

# 💀 8. Collapse-Level Companies (80–98% Layoffs)  
This is the list of companies that nearly **shut down**.

---
![Collapse Query](images/highest_collapsing_companies_query.png)
![Collapse Results](images/highest_collapsing_companies_results.png)

---
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

