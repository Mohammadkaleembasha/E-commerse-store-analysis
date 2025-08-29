## E-commerce Store Analysis (Power BI)

A Power BI report analyzing e-commerce orders, sales, profitability, product categories, geographies, and payment behavior.

### Datasets
- `Datasets/Orders.csv`: Order header info (one row per order)
- `Datasets/Details.csv`: Order line details, amounts, and product/payment attributes

### Data model
- Relationship: `Orders[Order ID]` 1 — * `Details[Order ID]`
- Date: `Orders[Order Date]` used as the primary date for time intelligence

### Schema

Orders.csv

| Column | Description |
|---|---|
| Order ID | Unique order identifier |
| Order Date | Order date (mixed formats: dd-mm-yyyy and m/d/yyyy) |
| CustomerName | Customer full name |
| State | Shipping/billing state |
| City | Shipping/billing city |

Details.csv

| Column | Description |
|---|---|
| Order ID | Foreign key to `Orders[Order ID]` |
| Amount | Line amount/revenue (numeric) |
| Profit | Line profit (can be negative) |
| Quantity | Units sold on the line |
| Category | High-level product category (e.g., Electronics, Furniture, Clothing) |
| Sub-Category | Product subcategory (e.g., Phones, Chairs, Saree) |
| PaymentMode | Payment method (e.g., COD, Credit Card, UPI, EMI, Debit Card) |

### Key measures (suggested)
- Total Sales: SUM of `Details[Amount]`
- Total Profit: SUM of `Details[Profit]`
- Profit Margin %: DIVIDE([Total Profit], [Total Sales])
- Total Quantity: SUM of `Details[Quantity]`
- Orders: DISTINCTCOUNT of `Orders[Order ID]`
- Avg Order Value (AOV): DIVIDE([Total Sales], [Orders])

### Example insights supported by the data
- Sales and profit trends by month/quarter
- Top categories/sub-categories by sales and profit
- State/City performance mapping
- Payment mode contribution to sales and profitability
- Product mix impact on margins (e.g., high return/low margin items)

### Report pages (recommended)
- Overview: Sales, Profit, Margin, Orders, AOV, date slicer
- Category Deep Dive: Category/Sub-Category matrices and contribution charts
- Geography: State/City map and tables
- Payment Analysis: PaymentMode breakdown and trends
- Customer Snapshot: Top customers by sales/profit

### Data preparation notes
- Ensure `Order Date` is parsed consistently. If formats vary (e.g., `24-01-2018` and `1/4/2018`), normalize to a single date type using Power Query (Change Type with Locale or a custom parse step).
- Validate numeric types for `Amount`, `Profit`, and `Quantity`.
- Remove leading/trailing spaces in `State`, `City`, `Category`, `Sub-Category`, and `PaymentMode`.

### How to use
1. Open `E-commerce store analysis.pbix` in Power BI Desktop.
2. If prompted, update the file paths for the two CSVs to match your local path:
   - `Datasets/Orders.csv`
   - `Datasets/Details.csv`
3. Refresh the model.
4. Review visuals and interact with slicers/filters.

### Folder structure
```
E-commerse store analysis/
  ├─ Datasets/
  │  ├─ Details.csv
  │  └─ Orders.csv
  └─ E-commerce store analysis.pbix
```

### Refresh and data source settings
- This project is designed for local CSV inputs. If publishing to Power BI Service, use a gateway or store data in a service-accessible location (e.g., OneDrive/SharePoint) and map the dataset credentials accordingly.



