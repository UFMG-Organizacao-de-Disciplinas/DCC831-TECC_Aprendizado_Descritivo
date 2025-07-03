# Credit Card Customer Segmentation Dataset

| Data Type | Column                           | Description                                             | Range            |                Range Explanation |
| :-------- | -------------------------------- | ------------------------------------------------------- | ---------------- | -------------------------------: |
| `float64` | BALANCE                          | Balance amount left in their account to make purchases  | [0, 19043.14]    |                                  |
| `float64` | BALANCE_FREQUENCY                | How frequently the Balance is updated                   | [0, 1.00]        |   Frequently updated? (1=Y, 0=N) |
| `float64` | CASH_ADVANCE                     | Cash in advance given by the user                       | [0, 47137.21]    |                                  |
| `float64` | CASH_ADVANCE_FREQUENCY           | How frequently the cash in advance being paid           | [0, 1.50]        |                                  |
| `float64` | CREDIT_LIMIT                     | Limit of Credit Card for user                           | [0, 30000.00]    |                                  |
| `float64` | INSTALLMENTS_PURCHASES           | Amount of purchase done in installment                  | [0, 22500.00]    |                                  |
| `float64` | MINIMUM_PAYMENTS                 | Minimum amount of payments made by user                 | [0, 76406.21]    |                                  |
| `float64` | ONEOFF_PURCHASES                 | Maximum purchase amount done in one-go                  | [0, 40761.25]    |                                  |
| `float64` | ONEOFF_PURCHASES_FREQUENCY       | How frequently Purchases are happening in one-go        | [0, 1.00]        | Frequently Purchased? (1=Y, 0=N) |
| `float64` | PAYMENTS                         | Amount of Payment done by user                          | [0, 50721.48]    |                                  |
| `float64` | PRC_FULL_PAYMENT                 | Percent of full payment paid by user                    | [0, 1.00]        |                                  |
| `float64` | PURCHASES                        | Amount of purchases made from account                   | [0, 49039.57]    |                                  |
| `float64` | PURCHASES_FREQUENCY              | How frequently the Purchases are being made             | [0, 1.00]        | Frequently Purchased? (1=Y, 0=N) |
| `float64` | PURCHASES_INSTALLMENTS_FREQUENCY | How frequently purchases in installments are being done | [0, 1.00]        |      Frequently Done? (1=Y, 0=N) |
| `int64`   | CASH_ADVANCE_TRX                 | Number of Transactions made with "Cash in Advanced"     | [0, 123]         |                                  |
| `int64`   | PURCHASES_TRX                    | Numbe of purchase transactions made                     | [0, 358]         |                                  |
| `int64`   | TENURE                           | Tenure of credit card service for user                  | [6, 12]          |                                  |
| `string`  | CUST_ID                          | Identification of Credit Card holder                    | [C10001, C19190] |                      Categorical |
