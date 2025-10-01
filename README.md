# Hotel Reservation Performance Dashboard

**Project name:** Hotel Reservation Performance Dashboard

---

## Project Overview

The project dataset contains **36 columns** and **119,390 rows**. The hotel booking data covers the period from **1 July 2015** to **31 August 2017**. Data was cleaned and missing values handled in order to build a decision-support dashboard.

**Objective:** Provide data-driven insights to support business strategy.

---

## Dataset Description

| Column Name                    | Description                                         |
| ------------------------------ | --------------------------------------------------- |
| hotel                          | Type of hotel (e.g., Resort Hotel or City Hotel)    |
| is_canceled                    | Whether the booking was canceled (1) or not (0)     |
| lead_time                      | Number of days between booking and arrival date     |
| arrival_date_year              | Year of arrival                                     |
| arrival_date_month             | Month of arrival (string, e.g., “July”)             |
| arrival_date_week_number       | Week number of year (1–53)                          |
| arrival_date_day_of_month      | Day of month (1–31)                                 |
| stays_in_weekend_nights        | Nights spent on weekends (Sat–Sun)                  |
| stays_in_week_nights           | Nights spent on weekdays (Mon–Fri)                  |
| adults                         | Number of adults                                    |
| children                       | Number of children                                  |
| babies                         | Number of babies                                    |
| meal                           | Type of meal booked (e.g., BB, FB, HB, SC)          |
| country                        | Country of origin of the guest                      |
| market_segment                 | Market segment (e.g., Direct, Corporate, Online TA) |
| distribution_channel           | Booking distribution channel (e.g., TA/TO, Direct)  |
| is_repeated_guest              | Whether the guest is a repeat guest (0/1)           |
| previous_cancellations         | Number of previous cancellations by guest           |
| previous_bookings_not_canceled | Number of previous non-canceled bookings            |
| reserved_room_type             | Reserved room type code                             |
| assigned_room_type             | Assigned room type code                             |
| booking_changes                | Number of changes/amendments to booking             |
| deposit_type                   | Deposit made (No Deposit, Non Refund, Refundable)   |
| agent                          | ID of booking agent (if any)                        |
| company                        | ID of company making the booking (if any)           |
| days_in_waiting_list           | Number of days booking was on waiting list          |
| customer_type                  | Type of customer (Transient, Contract, Group, etc.) |
| adr                            | Average Daily Rate (price per night per room)       |
| required_car_parking_spaces    | Number of car parking spaces required               |
| total_of_special_requests      | Number of special requests made by guest            |
| reservation_status             | Status (e.g., Canceled, Check-Out, No-Show)         |
| reservation_status_date        | Date of last status change                          |
| name                           | Guest name                                          |
| email                          | Guest email                                         |
| phone-number                   | Guest phone number                                  |
| credit_card                    | Credit card details (masked or encrypted)           |

---

## Tools & Technologies

* **Power BI** (Power Query / M, Data Modeling, DAX)
* Optional: Python / pandas for advanced cleaning or reproducible scripts

---

## Data Cleaning

1. **Renamed columns** to readable/consistent names.
2. **Fixed invalid ADR values**: negative ADR values were converted to positive (absolute value).
3. **Handled missing values** by replacing missing entries with the label `Unknown` (categorical) or using domain-appropriate defaults.
4. **Removed irrelevant columns** (PII or unused fields) such as `credit_card`, `phone-number`, `email`, `name` before analysis.

---

## Data Modeling

Built a date dimension and converted the main table into a star schema with the following dimensions:

* `Dim_Date` (calendar from 2015-07-01 to 2017-08-31)
* `Dim_Country`
* `Dim_Customer_Type`
* `Dim_Deposit_Type`
* `Dim_Distribution_Channel`
* `Dim_Hotel`
* `Dim_Market_Segment`
* `Dim_Meal_Plan`
* `Dim_Reservation_Status`
* `Dim_Room_Type`

Fact table: `Fact_Bookings`

Relationships: `Fact_Bookings` -> each `Dim_*` via surrogate keys; `Fact_Bookings[date_key]` -> `Dim_Date[date_key]`.

---

## Key Insights

### Booking Overview

* **Cancellation Rate:** 37.04%
* **Total Bookings:** 119,390
* **Avg Lead Time (days):** 104.01

**Cancellation Rate by Deposit Type**

* Non Refund: 66.26%
* No Deposit: 18.92%
* Refundable: 14.82%

**Booking Share by Hotel Type (Avg ADR by hotel type shown as share)**

* City Hotel: 68.71%
* Resort Hotel: 31.29%

### Customer & Market Insights

* **% repeated Guests:** 3.19%
* **Avg special requests:** 0.57
* **Avg required parking spaces:** 0.06

**Bookings by distribution channel**

* TA/TO: 97,870
* Direct: 14,645
* Corporate: 6,677
* GDS: 193
* Undefined: 5

**Bookings by market segment**

* Online TA: 56,477
* Offline TA/TO: 24,219
* Groups: 19,811
* Direct: 12,606
* Corporate: 5,295
* Complementary: 743

**Top country (by bookings)**

* Portugal: 48,590

### Customer Composition & Lead Time

* Avg adults: 1.86
* Avg children: 0.10
* Avg babies: 0.01

**Avg special requests by customer type**

* Contract: 0.73
* Group: 0.64
* Transient: 0.63
* Transient-Party: 0.33

**Bookings by lead-time buckets**

* 0–30 days: 38,047
* 30–60 days: 17,193
* 60–90 days: 12,726
* 90–120 days: 10,475

### Revenue & Operations

* **Total Revenue:** $42,720,000 (approx)
* **Avg booking changes / reservation:** 0.22
* **Avg waiting list days:** 2.23
* **Avg ADR:** $101.83

**Total Revenue by Year**

* 2015: $6,818,116.56
* 2016: $18,870,601.20
* 2017: $17,034,907.37

---

## Dashboards

1. **Booking Overview** — total bookings, cancellations, lead time, ADR, revenue trend, cancellation by deposit type.
2. **Customer & Market Insights** — repeated guests, distribution channel, market segments, country heatmap.
3. **Customer Composition** — party size, special requests, parking needs, lead-time buckets.
4. **Revenue & Operations** — revenue by year/month, ADR distribution, waiting list analysis, booking changes.

Each page includes slicers for `Hotel Type`, `Year`, `Market Segment`, `Distribution Channel`, and `Country`.

---

## Repo Structure (Suggested)

```
hotel-reservation-performance-dashboard/
├─ README.md
├─ data/
│  ├─ raw/
│  │  └─ hotel_bookings.csv  # original dataset (if allowed)
│  └─ processed/
│     └─ fact_bookings.parquet
├─ powerbi/
│  ├─ pbix/                  # final Power BI file(s)
│  ├─ pq_scripts/            # Power Query M scripts
│  └─ dax/                   # DAX measures
├─ notebooks/                # optional python notebooks for cleaning
│  └─ cleaning.ipynb
├─ docs/
│  └─ data_dictionary.md
├─ LICENSE
└─ .gitignore
```

> **Privacy note:** Do not commit raw files that contain PII (credit card, phone, email, name). Instead, use sanitized or sample subsets.

---

## Power Query (M) Examples

**1) Replace missing categorical values with `Unknown`:**

```m
= Table.ReplaceValue(Source, null, "Unknown", Replacer.ReplaceValue, {"agent"})
```

**2) Fix negative ADR values (make absolute):**

```m
= Table.TransformColumns(Source, {{"adr", each if _ < 0 then Number.Abs(_) else _, type number}})
```

**3) Create Lead-Time buckets (0-30,30-60,...):**

```m
= Table.AddColumn(#"Changed Type", "lead_time_bucket", each 
    if [lead_time] <= 30 then "0-30"
    else if [lead_time] <= 60 then "30-60"
    else if [lead_time] <= 90 then "60-90"
    else if [lead_time] <= 120 then "90-120"
    else ">120")
```

---

## Example DAX Measures

```dax
TotalBookings = COUNTROWS(Fact_Bookings)

CancellationRate = 
DIVIDE(
    CALCULATE([TotalBookings], Fact_Bookings[is_canceled] = 1),
    [TotalBookings]
)

AvgADR = AVERAGE(Fact_Bookings[adr])

TotalRevenue = SUMX(Fact_Bookings, Fact_Bookings[adr] * (Fact_Bookings[stays_in_weekend_nights] + Fact_Bookings[stays_in_week_nights]))
```

---

## How to Use

1. Clone the repo.
2. Place sanitized `hotel_bookings.csv` into `data/raw/` (or connect Power BI to source).
3. Run Power Query scripts (or open the provided pbix) to load fact & dimension tables.
4. Build relationships (or use provided pbix).
5. Explore dashboards with slicers and visuals.

---

## Conclusion & Recommendations

* Focus on **reducing cancellations** (high rate driven by non‑refundable and no‑deposit policies).
* Improve **direct booking** channels and incentivize repeat guests (repeat rate ~3.19%).
* Use lead-time segmentation for targeted offers.
* Add **data quality checks** into ETL (flag negatives, out-of-range values, PII filters).

---

## License

Choose an appropriate license (e.g., MIT) and add `LICENSE`.

---

## Next Steps (Optional)

* Add `Notebooks/` with reproducible cleaning code in Python.
* Add CI checks to verify no PII in committed CSVs.
* Publish a short `docs/` walkthrough for stakeholders.
