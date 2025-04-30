# Simple Connect Documentation

## Overview

Simple Connect is the simple way to export NetSuite Saved Searches into external software via REST. After setting up a Simple Connect User and a Simple Connect Search record, users can quickly and easily export the data they need.

---

## Getting Started

### Creating a Simple Connect User

1. Log in to NetSuite.
2. Navigate to **Setup > Simple Connect > New Simple Connect User**.
3. Set **NetSuite User Account** to the employee who will use this account.
   - The user will receive an email to complete the setup process.
4. Set the **Simple Connect Username**.
   - Choose a memorable username.
5. Click **Invite User**.
6. The employee will receive an email with a setup link. Click this link.
7. On the **Complete Simple Connect User Setup** screen, set the **Simple Connect Password**.
   - Password entry will be visible (not hidden), so be careful during screen sharing.
8. Click **Submit**.

*If the email isn't received, navigate to **Setup > Company > Sent Email List** to find the email.*

---

### Setting Up a Saved Search for Simple Connect

#### Example: Single Record per Row (e.g., Non-Inventory items)

1. Navigate to **Lists > Saved Searches > New**.
2. Select **Item**.
3. Name the search (suggested prefix: SC).
4. Set the search as **Public**.
5. Add the first **Criteria filter** as:
   - **Formula Numeric**: `{internalid}`
   - **Condition**: Greater than
   - **Value**: `0`
6. Add other desired criteria (e.g., Type is Non-inventory).
7. Navigate to **Results tab**.
8. First **SORT BY** field:
   - **Formula Numeric**: `{internalid}`
9. First result row:
   - **Formula Number**: `{internalid}`
   - **Custom Label**: `ROWKEY`
10. Add additional result rows as needed.
    ![image](https://github.com/user-attachments/assets/e32a32a6-cd55-402e-8a7f-b96e380c3f99)

12. Save the search.

#### Example: Multiple Rows per Record (e.g., Sales Order lines)

Use the same steps as above, but for the formula:

- Formula example for multiple lines:

```plaintext
({internalid}*10000) + TO_NUMBER({line})
```

Set this formula for both the criteria and the ROWKEY in results.

---

### Setting Up the Simple Connect Search Record

1. Navigate to **Setup > Simple Connect > Simple Connect Search > New**.
2. Populate the **Saved Search** field with the created search.
3. Add Simple Connect Users to the sublist and assign the execution role.
4. Save the record.
   - A URL will populate for accessing search data.

---

## Access Simple Connect via Excel

1. Open Excel.
2. Navigate to the **Data** tab.
3. Click **Get Data > From Other Sources > From Web**.
4. Paste the URL from the Simple Connect Search record.
5. Click **OK**.
6. Choose **Basic** on the authentication screen.
7. Enter your Simple Connect username and password.
8. Click **Connect**.
9. Once data preview appears, click **Load**.

### Tips for Simple Connect in Excel

#### Rename queries to match data clearly:
  - Double-click 'Queries', rename under 'Properties'.
    ![image](https://github.com/user-attachments/assets/a161ee5c-bd12-49c7-8423-b512558363ad)

#### Updating search results:
  - Double-click your query to open the power query editor.
  - Remove 'Changed Type' and 'Promoted Headers'.
    ![image](https://github.com/user-attachments/assets/116d9b44-8d01-45a6-ac17-f9863c83bf8c)
  - Under "Applied Steps", click on **Source** and check the contents in this step.
    ![image](https://github.com/user-attachments/assets/201fc109-c58f-4ed0-a5b7-16d43eed3665)

    The contents should look something like this:
    ```
    = Csv.Document(Web.Contents("https://examplesimpleconnecturl.com"),[Delimiter=",", Columns=20, Encoding=65001, QuoteStyle=QyoteStyle.None])
    ```
    If this step is specifying a format (delimiter, columns, etc.), this can all get removed. Modify the step so that it looks like this:
    ```
    = Csv.Document(Web.Contents("https://examplesimpleconnecturl.com"))
    ```
  - Click **Refresh**.
  - After refresh, click **Use First Row as Headers**.
  - If the power query is still using the old headers, delete **Changed Type** under "Applied Steps" again.
  - Click on **Promoted Headers** and refresh the query again.
  - Click **Close & Load**.

  #### Sharing your excel document with another SimpleConnect User
  - The user will need to authenticate within excel to access the connection using their own SimpleConnect credentials
  - Under the data tab navigate to Get Data—>Data Source Settings...
    ![image](https://github.com/user-attachments/assets/39a14a3b-e108-451f-92f8-ecbc74288ad0)
  - On the Data Source Settings page that appears, **right-click** on the connection string and click **Edit Permissions**
    ![image](https://github.com/user-attachments/assets/15dfbe8c-7de7-4d42-a971-3c39421e893d)
  - This will bring up the **edit permissions dialog**, from here, click **Edit...**
    ![image](https://github.com/user-attachments/assets/f1f3a53a-b60d-4a6b-b3aa-0ebe41f4fc66)
  - This will bring up the authentication screen. Typically this appears when the user first opens the document, but this is another way to get to this page.
    ![image](https://github.com/user-attachments/assets/618143fa-a3bd-4436-acd0-ede4bb7d2cd6)
  - This should be set to "Basic". The username will be the SimpleConnect username, and the password will be the password the user generated using the email link that was sent when their account was created.
  - Following these steps should allow the user to successfully connect and pull data using the shared document.

---

## Access Simple Connect via REST

- Make a GET request to the URL provided in the Simple Connect Search record.
- Authentication: Use Basic Auth with your username and password.
- Results returned in CSV format.


