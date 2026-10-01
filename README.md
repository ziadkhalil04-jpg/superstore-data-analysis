# 📊 Superstore Orders — Data Cleaning & Exploratory Analysis

An end-to-end data cleaning and exploratory data analysis (EDA) project on the **Global Superstore orders dataset** (2011–2014), built with Python, Pandas and Matplotlib.

The goal: turn a raw orders file into a clean dataset, then find out **what drives sales and profit — and where the business is losing money.**

---

## 🎯 Project Goals

- Clean and prepare the raw orders data for analysis
- Identify top products, customers and states by sales and profit
- Find loss-making areas and understand what causes them

---

## 📁 Dataset

| Item | Detail |
|---|---|
| Rows | 13,297 order lines |
| Orders | 6,717 |
| Customers | 795 |
| Period | 2011 – 2014 |
| Markets | APAC, EU, US, LATAM, EMEA, Africa, Canada |
| Key columns | order/ship date, ship mode, customer, segment, state, country, market, category, sub-category, product, sales, quantity, discount, profit, shipping cost, order priority |

---

## 🧹 Data Cleaning Steps

1. Loaded the raw CSV and inspected structure with `info()` and `describe()`
2. Checked for **missing values** and **duplicate rows** (none found — dataset was already complete)
3. Converted `discount` from text (e.g. `"20.0%"`) to a numeric value using `pd.to_numeric`
4. Parsed `order_date` and `ship_date` as dates (day-first format `dd/mm/yyyy`)
5. Created a new column `shipping_days` = ship date − order date
6. Reordered columns and sorted by market, state and order priority
7. Exported the clean dataset to `data/DataClean.csv`

```python
df['discount'] = pd.to_numeric(df['discount'].str.rstrip('%'), errors='coerce') / 100

df['order_date'] = pd.to_datetime(df['order_date'], dayfirst=True)
df['ship_date']  = pd.to_datetime(df['ship_date'],  dayfirst=True)
df['shipping_days'] = (df['ship_date'] - df['order_date']).dt.days
```

---

## 🔍 Key Findings

### Overall performance
- **Total sales: $3.25M** · **Total profit: $401K** · **Profit margin: 12.4%**
- Sales grew every year, from **$606K (2011)** to **$1.05M (2014)**
- But the margin did not grow with it: **2013 was the best year (13.9%)**, and 2014 dropped to **11.3%**
- **~24% of order lines (3,250) lost money**

### Category & product
- **Technology** is the most profitable category ($185K profit, 14.9% margin)
- **Furniture** brings $1.01M in sales but only **$81K profit (8% margin)**
- **Tables** is the only sub-category with a net loss: **−$11K** on $186K in sales
- Top sub-categories by profit: Copiers ($79K), Phones ($48K), Appliances ($41K)
- Top single product (by sales + country): **Canon imageCLASS 2200 Advanced Copier** (US) — $17.5K

### Geography
- Highest profit by market: **APAC ($126K)**, **EU ($104K)**, **US ($85K)**
- **EMEA** has a weak margin (~6%), while **Canada** has a small volume but a 25% margin
- Top states by profit: **England ($25.4K)**, **New York ($24.1K)**, **California ($20.4K)**
- Biggest losses: **Lagos (−$9.9K)**, **Texas (−$8.9K)**, **Istanbul (−$8.8K)**

### Customers
- Top customers by sales: **Tamara Chand ($22.9K)**, Todd Sumrall ($15.3K), Bart Watters ($15.1K)

### 💡 Discounts and losses
Profit falls sharply as discounts increase:

| Discount level | Total profit | Avg. profit per line | Order lines |
|---|---|---|---|
| No discount | +$472.7K | +$63.0 | 7,504 |
| Up to 20% | +$130.0K | +$45.6 | 2,849 |
| 20% – 40% | −$52.1K | −$43.6 | 1,196 |
| Above 40% | −$149.7K | −$85.7 | 1,748 |

About **50% of Tables order lines carry a discount above 20%**, compared with ~22% for all other sub-categories — a likely contributor to the losses (this is an association, not proof of cause).

### 🚚 Shipping
- Average shipping time is **~3.6 days** (max 7 days)
- By ship mode: Same Day ≈ 0 days, First Class ≈ 2.1, Second Class ≈ 3.1, Standard Class ≈ 4.8

---

## ✅ Recommendations

1. **Cap discounts at ~20%.** Discounts above that level are associated with consistent losses.
2. **Review Table pricing and discount policy** — it is the only loss-making sub-category.
3. **Investigate loss-making locations** (Lagos, Texas, Istanbul) for pricing, shipping or discount issues.
4. **Focus growth on Technology and APAC/EU** where margins are strongest.

---

## 🛠 Tools & Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook

---

## 📂 Repository Structure

```
superstore-data-analysis/
├── README.md
├── Data_Clean.ipynb      # full notebook with charts and insights
├── data_clean.py         # same analysis as a runnable Python script
├── requirements.txt
├── images/               # chart images used in this README
└── data/
    ├── SuperStoreOrders.csv   # raw data (add this file)
    └── DataClean.csv          # cleaned data (output)
```

---

## ▶️ How to Run

```bash
git clone https://github.com/<your-username>/superstore-data-analysis.git
cd superstore-data-analysis
pip install -r requirements.txt
```

Then either open the notebook:
```bash
jupyter notebook Data_Clean.ipynb
```
or run the script (cleans the data, saves `data/DataClean.csv` and all charts in `images/`):
```bash
python data_clean.py
```

> Make sure the raw file `SuperStoreOrders.csv` is inside the `data/` folder first.

`requirements.txt`:
```
pandas
numpy
matplotlib
openpyxl
```

---

## 📸 Charts

### Top 10 Products by Sales
![Top 10 Products by Sales](images/top_products.png)

### Top 10 States by Profit
![Top 10 States by Profit](images/top_states.png)

### Top 10 Customers by Sales
![Top 10 Customers by Sales](images/top_customers.png)

### Profit by Sub-Category
![Profit by Sub-Category](images/profit_by_subcategory.png)

### Profit by Discount Level
![Profit by Discount Level](images/profit_by_discount.png)

### Sales and Profit per Year
![Sales and Profit per Year](images/yearly_trend.png)

---

## 👤 Author

**Ziad ElSayed** — Data Analyst, Alexandria, Egypt

- LinkedIn: [www.linkedin.com/in/ziad-khalil-dev]
- GitHub: [https://github.com/ziadkhalil04-jpg]
