Here’s a **Confluence-style functional test documentation template** tailored for your scenario — adding a new column `column_ppi` in existing views. You can copy-paste this into your Confluence page and adjust the view names and SQL as needed.

---

## 🧪 Functional Test Documentation – Addition of `column_ppi` to Views

### 🔍 Objective

To validate the successful integration of the new column `column_ppi` into existing views without impacting existing functionality, and to ensure its values are populated as expected.

---

### 📋 Change Summary

| Item           | Description                                                                    |
| -------------- | ------------------------------------------------------------------------------ |
| Change Type    | Enhancement                                                                    |
| Component      | Data Warehouse Views                                                           |
| Column Added   | `column_ppi`                                                                   |
| Data Type      | `STRING` (Adjust if needed)                                                    |
| Source         | Derived from base table `xyz_base_table.column_ppi` (or specify actual source) |
| Views Affected | `view_customer_summary`, `view_order_details` (Add all impacted views)         |

---

### ✅ Test Scenarios & Functional Test Cases

#### 1. **Schema Validation – `column_ppi` Exists**

| Test Case ID    | TC001                                                          |
| --------------- | -------------------------------------------------------------- |
| Description     | Validate that `column_ppi` exists in all updated views         |
| SQL/Steps       | `SELECT column_ppi FROM <view_name> LIMIT 1;`                  |
| Expected Result | Query should return without error and column should be present |
| Views Covered   | All impacted views                                             |
| Status          | Pending / Pass / Fail                                          |

---

#### 2. **Data Population – Not Null Check**

| Test Case ID    | TC002                                                              |
| --------------- | ------------------------------------------------------------------ |
| Description     | Ensure `column_ppi` is not null for records where data is expected |
| SQL/Steps       | `SELECT COUNT(*) FROM <view_name> WHERE column_ppi IS NULL;`       |
| Expected Result | Count should be 0 for valid data scenarios                         |
| Notes           | If nulls are expected in some rows, mention business rules here    |
| Status          | Pending / Pass / Fail                                              |

---

#### 3. **Data Accuracy – Value Match with Base Table**

| Test Case ID | TC003                                                                |
| ------------ | -------------------------------------------------------------------- |
| Description  | Validate that values in `column_ppi` match those in the source table |
| SQL/Steps    |                                                                      |

```sql
SELECT v.column_ppi, b.column_ppi 
FROM <view_name> v 
JOIN <base_table_name> b ON v.id = b.id 
WHERE v.column_ppi != b.column_ppi;
```

\| Expected Result | Result set should be empty |
\| Status       | Pending / Pass / Fail |

---

#### 4. **Backward Compatibility**

| Test Case ID    | TC004                                                                            |
| --------------- | -------------------------------------------------------------------------------- |
| Description     | Ensure existing queries using the view are not impacted                          |
| SQL/Steps       | Run previously known working queries (with `SELECT *` or excluding `column_ppi`) |
| Expected Result | Queries return same results as before addition                                   |
| Status          | Pending / Pass / Fail                                                            |

---

### 🛠 Additional Notes

* Ensure that access privileges to new column follow existing security model.
* Coordinate with consumers of the views (e.g. downstream reports or dashboards) to verify if any changes are needed.
* Check for nullability constraints or default values for `column_ppi`.

---

### 📅 Test Execution Tracker

| Tester          | Date         | Test Case ID(s) | Result      | Remarks          |
| --------------- | ------------ | --------------- | ----------- | ---------------- |
| *Assigned Name* | *yyyy-mm-dd* | TC001–TC004     | Pass / Fail | Any observations |

---

Let me know if you want to include screenshots, sample data, or test evidence tables as well.


Thanks for the clarification! Based on your documentation style, here's the functional test documentation in your **table format** for the change involving the addition of `column_ppi` to existing views.

---

### 🧪 Functional Test Documentation – `column_ppi` Addition

| **Source FDP**   | **Source FDP Data Attribute** | **Given When Then (GWT)**                                                                                                                                                   | **Description**                                                  | **SQL / SQL Filename**                                                                                                          | **XRAY Artifact** | **DIM Issue Raised**         |
| ---------------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------------- | ---------------------------- |
| `xyz_base_table` | `column_ppi`                  | **Given** the base table `xyz_base_table` has the `column_ppi`<br>**When** the view `<view_name>` is queried<br>**Then** `column_ppi` should be present in the schema       | Validate if `column_ppi` is added to all required views          | `SELECT column_ppi FROM <view_name> LIMIT 1;`                                                                                   | `XRAY-12345`      | No                           |
| `xyz_base_table` | `column_ppi`                  | **Given** valid data is present in the base table for `column_ppi`<br>**When** data flows into the view<br>**Then** `column_ppi` should not be null (as per business rules) | Validate `column_ppi` is populated correctly in the view         | `SELECT COUNT(*) FROM <view_name> WHERE column_ppi IS NULL;`                                                                    | `XRAY-12346`      | No                           |
| `xyz_base_table` | `column_ppi`                  | **Given** values in `column_ppi` are transformed correctly (or passed as-is)<br>**When** the view is queried<br>**Then** the values should match source accurately          | Check data correctness by comparing with base table              | `SELECT v.column_ppi, b.column_ppi FROM <view_name> v JOIN xyz_base_table b ON v.id = b.id WHERE v.column_ppi != b.column_ppi;` | `XRAY-12347`      | No                           |
| `xyz_base_table` | `column_ppi`                  | **Given** consumers use existing views<br>**When** the views are queried after the addition<br>**Then** there should be no impact to existing queries                       | Backward compatibility check to ensure legacy queries don’t fail | Use previously validated queries from test suite or dashboards                                                                  | `XRAY-12348`      | No                           |
| `xyz_base_table` | `column_ppi`                  | **Given** the column is sensitive (if PII)<br>**When** views are queried by roles<br>**Then** access should comply with security model                                      | Validate column access permissions and masking (if applicable)   | Security test script or view GRANTS                                                                                             | `XRAY-12349`      | If access rules missing, Yes |

---

Let me know:

* If the `XRAY Artifact` values should be updated with actual IDs.
* If `DIM Issue Raised` should be marked for any specific validation failure.
* If you'd like a downloadable CSV or Confluence table markup version.
