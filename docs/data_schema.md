# Data Schema

## Dataverse Table: Orders

Source: data/orders.xlsx (Sheet1, 10 seed records)

---

### Columns

| Column Name | Data Type | Example Value | Notes |
|---|---|---|---|
| Order Number | Text | ORD-1001 | Primary identifier, format: ORD-XXXX |
| Product Name | Text | Wireless Keyboard | Name of product ordered |
| Quantity | Whole Number | 25 | Number of units ordered |
| Order Date | Date Only | 2024-01-05 | Date order was placed |
| Expected Delivery Date | Date Only | 2024-05-05 | Expected arrival date |
| Delivery Status | Text | Pending | Current values: Pending |

---

### Seed Data (Orders.xlsx contents)

| Order Number | Product Name | Quantity | Order Date | Expected Delivery Date | Delivery Status |
|---|---|---|---|---|---|
| ORD-1001 | Wireless Keyboard | 25 | 2024-01-05 | 2024-05-05 | Pending |
| ORD-1002 | Bluetooth Mouse | 40 | 2024-02-05 | 2024-06-05 | Pending |
| ORD-1003 | Laptop Stand | 15 | 2024-03-05 | 2024-07-05 | Pending |
| ORD-1004 | USB-C Docking Station | 30 | 2024-04-05 | 2024-08-05 | Pending |
| ORD-1005 | Noise Cancelling Headset | 10 | 2024-05-05 | 2024-09-05 | Pending |
| ORD-1006 | External Hard Drive | 20 | 2024-06-05 | 2024-10-05 | Pending |
| ORD-1007 | Office Chair | 5 | 2024-07-05 | 2024-11-05 | Pending |
| ORD-1008 | Monitor 27-inch | 12 | 2024-08-05 | 2024-12-05 | Pending |
| ORD-1009 | Ergonomic Desk | 8 | 2024-09-05 | 2024-07-15 | Pending |
| ORD-1010 | Smart Speaker | 18 | 2024-10-05 | 2024-12-14 | Pending |

---

### Dataverse Column Mapping (Excel to Dataverse)

When importing Orders.xlsx into Dataverse, map columns as follows:

| Excel Column | Dataverse Column | Dataverse Type |
|---|---|---|
| Order Number | Order Number | Single line of text |
| Product Name | Product Name | Single line of text |
| Quantity | Quantity | Whole Number |
| Order Date | Order Date | Date Only |
| Expected Delivery Date | Expected Delivery Date | Date Only |
| Delivery Status | Delivery Status | Single line of text |

---

### Agent Flow Parameters

The Power Automate Agent Flow (Step 3) accepts these input parameters for creating new records:

| Parameter | Type | Maps To |
|---|---|---|
| Product Name | Text | Product Name column |
| Order Number | Text | Order Number column |
| Quantity | Number | Quantity column |
| Delivery Status | Text | Delivery Status column |

Note: Order Date and Expected Delivery Date are not required Agent Flow parameters per project spec.
