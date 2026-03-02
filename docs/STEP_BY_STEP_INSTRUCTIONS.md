# Step-by-Step Build Instructions

## Order Fulfillment Tracking System

This document provides exact click-by-click instructions for every step of the project.
All URLs, button labels, field values, and text inputs are specified exactly as needed.

---

## Prerequisites

Before starting, confirm you have access to:

- A Microsoft 365 account with Power Apps, Power Automate, and Copilot Studio licenses
- Access to Power Platform Admin Center
- The file `data/orders.xlsx` from this repository

---

## Step 0: Verify or Create a US-Based Environment

### What this is
Power Platform runs in regional environments. The project requires United States region.

### Instructions

1. Open your browser and go to: `https://admin.powerplatform.microsoft.com`
2. Sign in with your Microsoft 365 account
3. In the left navigation, click **Environments**
4. Look at the list of environments shown
   - If you see an environment with **Region = United States**, you can use it
   - If none exist or all are in other regions, proceed to create one

### Creating a new US environment (if needed)

5. Click **+ New** in the top menu bar
6. Fill in the form:
   - **Name**: `Order Management Dev` (or any name you prefer)
   - **Region**: `United States`
   - **Type**: `Developer` (if available on your license) or `Trial`
   - **Purpose**: Leave default or type `Udacity project environment`
   - **Create a database for this environment**: Toggle to `Yes`
   - **Language**: `English`
   - **Currency**: `USD`
7. Click **Next**
8. On the database settings screen:
   - **Enable Dynamics 365 apps**: `No` (unless required)
   - **Deploy sample apps and data**: `No`
9. Click **Save**
10. Wait for the environment to finish provisioning (status will change from "Preparing" to "Ready")

### Screenshot to take
Take a screenshot of the environment list showing your US-based environment with status "Ready".

---

## Step 1: Create the Dataverse Table from Orders.xlsx

### What this is
Import the Excel file as a new Dataverse table. This becomes the data store for the app.

### Instructions

1. Go to: `https://make.powerapps.com`
2. In the top-right corner, click the **environment selector** (shows current environment name)
3. Select your **US-based environment** from the list
4. In the left navigation, click **Tables**
5. Click **+ New table** in the top menu bar
6. From the dropdown that appears, select **Import an Excel file**
7. In the dialog that opens, click **Browse** (or drag and drop)
8. Navigate to the `data/` folder of this project and select `orders.xlsx`
9. Click **Open**
10. Wait for the file to upload and parse (a preview will appear)

### Column Mapping (Critical)

Once the preview loads, verify that each column is mapped correctly:

| Excel Column | Dataverse Column Name | Data Type to Set |
|---|---|---|
| Order Number | Order Number | Single line of text |
| Product Name | Product Name | Single line of text |
| Quantity | Quantity | Whole Number |
| Order Date | Order Date | Date Only |
| Expected Delivery Date | Expected Delivery Date | Date Only |
| Delivery Status | Delivery Status | Single line of text |

If any column shows the wrong data type, click on it and change it.

11. After verifying all mappings, click **Create** (or **Import**)
12. The system will create the table and import all 10 records
13. Wait for the import to complete

### Verify the import

14. After creation, you will be taken to the table editor
15. Click **Edit** (or open the table view) to see the rows
16. Confirm all 10 records are present:
    - ORD-1001 through ORD-1010
    - All Delivery Status values show "Pending"

### Screenshot to take
Screenshot of the Dataverse table showing the data rows and the table name/properties panel.

---

## Step 2: Create the Canvas App

### What this is
Build a Canvas App directly from the Dataverse table. Power Apps auto-generates three screens
(Browse, Detail, Edit). You will then add a WelcomeScreen and configure navigation.

### Part A: Generate the initial app from the table

1. In the left navigation, click **Tables**
2. Click on your **Orders** table
3. In the top menu, click **Create apps** (or click the three-dot menu and select **Create app**)
4. Select **Canvas app**
5. Give the app a name: `Order Management App`
6. Select **Phone** layout (or Tablet - your choice)
7. Click **Create**
8. Power Apps Studio will open with three auto-generated screens:
   - `BrowseScreen1` - gallery of all orders with search
   - `DetailScreen1` - read-only view of a selected record
   - `EditScreen1` - form for creating and editing records

### Part B: Add the WelcomeScreen

9. In the left Tree View panel, click the **+** icon next to Screens
   (or go to the top menu: **Home** tab > **New screen** > **Blank**)
10. A new blank screen is added - it appears at the bottom of the tree
11. Click the new screen in the Tree View to select it
12. Press **F2** (or double-click the screen name) to rename it
13. Type: `WelcomeScreen`
14. Press **Enter**

### Part C: Add an Image to WelcomeScreen

15. With WelcomeScreen selected, go to the **Insert** tab in the top menu
16. Click **Media** > **Image**
17. An image control appears on the canvas
18. In the right Properties panel, under **Image source**, click **Add an image file**
19. Upload any image (a company logo, placeholder image, or any relevant image)
    - If you have no image, you can use a built-in Power Apps icon:
      in Properties, set the Image property to one of the built-in values like
      `SampleImage` (Power Apps has built-in sample images)
20. Resize and position the image at the top-center of the screen using the drag handles

### Part D: Add the Personalized Greeting Label

21. With WelcomeScreen still selected, go to **Insert** tab > **Text** > **Label**
22. A text label appears on the canvas
23. Click the label to select it
24. In the formula bar at the top, click and set the **Text** property to:
    ```
    "Welcome, " & User().FullName
    ```
25. Style the label (optional): increase font size to 24+, center-align, adjust color in the right panel

### Part E: Add the Navigation Button

26. With WelcomeScreen selected, go to **Insert** tab > **Button**
27. A button appears on the canvas
28. Click the button to select it
29. In the right Properties panel, set the **Text** property to:
    ```
    "View Orders"
    ```
    (or any label that makes sense, such as "Get Started")
30. With the button selected, find the **OnSelect** property in the formula bar dropdown
31. Click the formula bar and enter:
    ```
    Navigate(BrowseScreen1, ScreenTransition.Fade)
    ```
    Note: if your browse screen is named differently, use that exact name.
32. Position the button below the greeting label

### Part F: Move WelcomeScreen to the Top of the Tree View

33. In the left Tree View, right-click on **WelcomeScreen**
34. Select **Move up** - click this repeatedly until WelcomeScreen is at the very top of the list
    (It must be above BrowseScreen1, DetailScreen1, and EditScreen1)
35. Confirm WelcomeScreen is the first item in the Tree View

### Part G: Add a Back Icon to BrowseScreen

36. In the Tree View, click **BrowseScreen1** to select it
37. Look for the back arrow/icon that was auto-generated at the top of the screen
    - If one already exists, click it and check its **OnSelect** property
    - If none exists, go to **Insert** tab > **Icons** > search for "Back" > click the back arrow icon
38. With the Back icon selected, set the **OnSelect** property in the formula bar to:
    ```
    Navigate(WelcomeScreen, ScreenTransition.Back)
    ```

### Part H: Test, Save, and Publish

39. Click the **Play** button (triangle icon, top right) to test the app
40. Verify:
    - App opens to WelcomeScreen
    - Greeting shows your name
    - Button navigates to BrowseScreen
    - Back icon on BrowseScreen returns to WelcomeScreen
    - Orders gallery shows data from Dataverse
    - Search bar filters records
    - Selecting a record opens DetailScreen (read-only)
    - Edit button opens EditScreen (form)
41. Press **Escape** to exit preview mode
42. Click **File** > **Save** (or Ctrl+S)
43. Click **Publish** > **Publish this version**

### Screenshots to take
- WelcomeScreen showing the image, greeting text with your name, and button
- BrowseScreen showing the back icon
- BrowseScreen showing the search bar being used (type something in the search box)
- DetailScreen showing a selected record in read-only view
- EditScreen showing the form for creating a new record (click the + icon in the gallery)
- Screenshot of the Power FX formula `Navigate(BrowseScreen1, ScreenTransition.Fade)` in the formula bar

---

## Step 3: Create the Power Automate Agent Flow

### What this is
An Agent Flow is a special type of Power Automate flow that Copilot agents can call.
It accepts structured parameters, creates a Dataverse record, and returns a response.

### Instructions

1. Go to: `https://make.powerautomate.com`
2. In the top-right corner, confirm you are in the **same US-based environment**
3. In the left navigation, click **+ Create**
4. Look for **Agent flow** (it may appear under "Start from blank" section)
   - If you see an option labeled **Agent flow**, click it
   - Alternative path: click **New flow** > **Agent flow**
5. A new flow opens with an **Agent trigger** block at the top

### Part A: Configure the Agent Trigger (Input Parameters)

6. Click on the **Agent trigger** block to expand it
7. Click **+ Add an input** to add the first parameter:
   - Click the type selector and choose **Text**
   - For the input name, type: `Product Name`
8. Click **+ Add an input** again for the second parameter:
   - Type: `Text`
   - Name: `Order Number`
9. Click **+ Add an input** again:
   - Type: **Number**
   - Name: `Quantity`
10. Click **+ Add an input** again:
    - Type: `Text`
    - Name: `Delivery Status`

You should now have 4 input parameters defined in the trigger.

### Part B: Add the Dataverse Action (Create Record)

11. Click the **+** button below the Agent trigger block
12. Click **Add an action**
13. In the search bar, type: `Dataverse`
14. From the results, click **Microsoft Dataverse**
15. Click **Add a new row**
16. In the action configuration:
    - **Table name**: Click the dropdown and select your **Orders** table
    - After selecting the table, additional column fields will appear

17. Map the parameters to columns:
    - **Order Number** field: click inside it, then click the lightning bolt (dynamic content) icon
      and select **Order Number** from the Agent trigger inputs
    - **Product Name** field: select **Product Name** from dynamic content
    - **Quantity** field: select **Quantity** from dynamic content
    - **Delivery Status** field: select **Delivery Status** from dynamic content

Note: Leave Order Date and Expected Delivery Date blank (not required per project spec).

### Part C: Add the Response Action

18. Click **+** below the Dataverse action
19. Click **Add an action**
20. Search for: `Respond to agent`
21. Click **Respond to agent** (or **Return value(s) to the virtual agent**)
22. In the response configuration:
    - Click **+ Add an output**
    - Type: **Text**
    - Name: `Response`
    - Value: Click inside the value field, then type:
      ```
      Product
      ```
      then click the lightning bolt icon and select **Product Name** from the Agent trigger,
      then continue typing:
      ```
       has been successfully added to the orders list.
      ```
      The final value should look like: `Product [Product Name dynamic value] has been successfully added to the orders list.`

### Part D: Save and Name the Flow

23. Click the **Save** button (top right or top menu)
24. Before or after saving, click the flow name at the top (default is "Untitled")
25. Rename it to: `Create Order Flow`
26. Click **Save** again

### Screenshots to take
- The Agent trigger block showing all 4 input parameters (Product Name, Order Number, Quantity, Delivery Status)
- The Dataverse "Add a new row" action showing the table and mapped parameters
- The "Respond to agent" action showing the response text with the Product Name parameter

---

## Step 4: Configure the Copilot Agent

### What this is
Create a new Copilot agent in Copilot Studio named "Order Record Assistant".
Add a topic that triggers when a user wants to create an order, calls the Agent Flow,
and sends the response back to the user.

### Part A: Create the Agent

1. Go to: `https://copilotstudio.microsoft.com`
2. Confirm you are in the correct **US-based environment** (top right selector)
3. Click **+ Create** or **New agent** in the left navigation
4. Choose to create from scratch (not a template)
5. Fill in the agent details:
   - **Name**: `Order Record Assistant`
   - **Description**: `An AI assistant that helps users create and manage orders in the Order Fulfillment Tracking System. Users can create new order records through conversation.`
   - **Instructions**: (paste the following)
     ```
     You are an Order Record Assistant for the company's Order Fulfillment Tracking System.
     Your primary role is to help users create new order records.
     When a user wants to create an order, collect the following information:
     - Product Name
     - Order Number (format: ORD-XXXX)
     - Quantity (a whole number)
     - Delivery Status (default to "Pending" if not specified)
     Once you have all required information, call the Create Order Flow to add the record.
     Confirm the order was created by sharing the response from the flow.
     ```
6. Click **Create** to create the agent

### Part B: Create a New Topic

7. In the left navigation of Copilot Studio, click **Topics**
8. Click **+ Add a topic** > **From blank**
9. A new topic opens in the topic editor
10. At the top, click the topic name (default "Untitled") and rename it to:
    `Create New Order`

### Part C: Add Trigger Phrases

11. In the topic editor, click on the **Trigger** node (it should already be there)
12. Under the trigger node, find the **Phrases** section
13. Click **+ Add phrases** and add each of the following (press Enter after each):
    - `I want to create a new order`
    - `create an order`
    - `add a new order`
    - `place an order`
    - `I need to add an order`
    - `new order`
    - `add order`
14. Click the checkmark or Save to confirm the phrases

### Part D: Add an Action Node to Call the Agent Flow

15. Below the Trigger node in the topic canvas, click the **+** button to add a node
16. From the dropdown, click **Call an action**
17. A list of available flows appears - click on **Create Order Flow**
    (the flow you created in Step 3)
18. The action node appears showing the 4 input parameters:
    - **Product Name**: If you want Copilot to ask for this, click the input field
      and set it to ask the user. You can also use Copilot's built-in entity extraction.
      For simplicity: click the field and select **Ask the user** or leave as a variable
    - **Order Number**: Same approach
    - **Quantity**: Same approach
    - **Delivery Status**: Set a static value of `Pending` (type it directly)
      or allow the user to specify it

    For each input where you want Copilot to gather information from the user:
    - Click the field
    - Select **Ask the agent** or configure it to prompt the user

    The simplest configuration: connect each parameter directly to a question node
    that collects the value, then pass it to the flow.

### Part E: Add a Message Node to Send the Response

19. Below the action node, click **+** to add another node
20. Select **Send a message**
21. In the message text box, type:
    ```
    Your order has been created.
    ```
22. Then click the **{x}** variable icon or the **Insert variable** option
23. Select the output from the Create Order Flow (it should appear as the `Response` variable
    from the flow's output)
24. The message node should show something like:
    `Your order has been created. {Topic.Response}` or similar variable syntax

25. Click **Save** (top right)

### Part F: Test the Agent

26. In the top-right area, click **Test** to open the test chat panel
27. Type one of your trigger phrases, for example:
    ```
    I want to create a new order
    ```
28. Follow the conversation, providing:
    - Product Name: `Test Product`
    - Order Number: `ORD-9999`
    - Quantity: `5`
    - Delivery Status: `Pending`
29. Verify the agent confirms the order was created

---

## Step 5: Publish and Share the Copilot Agent

### Part A: Publish the Agent

1. In Copilot Studio, with your agent open, click **Publish** in the top-right area
2. A confirmation dialog appears - click **Publish** to confirm
3. Wait for publishing to complete (status changes to "Published")

### Part B: Share with a User

4. In the left navigation, click **Settings** > **Security** (or look for a **Share** button)
5. Alternatively, go to the agent's main page and look for **Share** in the top menu
6. In the sharing dialog, type the email address of at least one other user
7. Set their permission to **User** (not Owner)
8. Click **Share** or **Add**
9. The user receives an invitation

### Part C: Add to Microsoft Teams Channel

10. In the left navigation of Copilot Studio, click **Channels**
11. Click **Microsoft Teams**
12. Click **Add to Teams** or **Turn on Teams**
13. Follow the prompts to enable the agent in Teams
14. Click **Open in Teams** to launch the agent in Teams for testing

### Part D: Test in Microsoft Teams

15. Open Microsoft Teams (desktop app or `https://teams.microsoft.com`)
16. Find the agent in the Apps section or search for "Order Record Assistant"
17. Start a conversation with the agent
18. Type: `I want to create a new order`
19. Follow the conversation to create a test order
20. Take a screenshot of the full conversation

### Part E: Test in Microsoft 365 Copilot Chat

21. Open Microsoft 365 Copilot Chat: `https://m365.cloud.microsoft/chat`
    (or access via Microsoft 365 apps menu > Copilot)
22. Look for the agent in the right panel or click the "+" to add an agent
23. Select "Order Record Assistant"
24. Start a conversation with the agent
25. Type: `create an order`
26. Complete the order creation conversation
27. Take a screenshot of the full conversation

### Screenshots to take
- The sharing dialog showing at least one user has been added
- Teams conversation with the agent showing a full order creation dialogue
- Copilot Chat conversation with the agent showing a full order creation dialogue
- The new record that was created (you will see this in Step 6)

---

## Step 6: Test the App and Agent Integration

### What this is
Verify end-to-end: use Copilot to create a record, then open the Canvas App to confirm
the record appears.

### Instructions

1. Open the Canvas App by going to: `https://make.powerapps.com`
2. In the left navigation, click **Apps**
3. Find **Order Management App** and click **Play** (the triangle icon)
4. The app opens to the WelcomeScreen
5. Click your navigation button to go to BrowseScreen
6. Note the current list of orders (you should see ORD-1001 through ORD-1010 plus any test records)

7. Switch to Microsoft Teams or Copilot Chat
8. Open the Order Record Assistant agent
9. Type: `I want to create a new order`
10. Provide these values when prompted:
    - Product Name: `Mechanical Keyboard`
    - Order Number: `ORD-2001`
    - Quantity: `3`
    - Delivery Status: `Pending`
11. Confirm the agent responds with a success message

12. Switch back to the Canvas App in your browser
13. Press **F5** or click the **Refresh** button in the browser (not the app)
14. Alternatively, close and reopen the app from the Apps list
15. Navigate to BrowseScreen - you should now see the new record `ORD-2001` / `Mechanical Keyboard`

### Screenshots to take
- The Canvas App BrowseScreen showing the new record that was just created via Copilot
- The Copilot Agent conversation showing the successful order creation response
- Any Copilot component visible within the app (if you added a Copilot Chat component to the app canvas)

---

## Step 7: Create and Export the Solution

### What this is
A Power Platform Solution bundles all components (app, agent, flow, table) into a
single exportable package for submission.

### Part A: Create the Solution

1. Go to: `https://make.powerapps.com`
2. Confirm you are in the correct US environment
3. In the left navigation, click **Solutions**
4. Click **+ New solution** in the top menu
5. Fill in the form:
   - **Display name**: `Order Management Solution`
   - **Name**: `OrderManagementSolution` (auto-populated, no spaces)
   - **Publisher**: Select an existing publisher or create a new one
     - To create new: click **+ New publisher**
       - Display name: Your name or organization name
       - Name: your name without spaces (e.g., `RodolfoLerma`)
       - Prefix: 3-5 characters (e.g., `rlc`)
     - Click **Save**
   - **Version**: `1.0.0.0`
6. Click **Create**

### Part B: Add the Canvas App

7. You are now inside the solution - click **+ Add existing** > **App** > **Canvas app**
8. Find and select **Order Management App**
9. Click **Add**
10. A prompt may appear asking to include required objects - click **Add required objects**
    (this should automatically include the Dataverse table)

### Part C: Add the Dataverse Table (if not auto-added)

11. If the Orders table was not added automatically:
    - Click **+ Add existing** > **Table**
    - Search for and select your **Orders** table
    - In the dialog, choose to include **All objects** or select specific ones
    - Click **Add**

### Part D: Add the Copilot Agent

12. Click **+ Add existing** > **Chatbot** (or **Copilot agent**)
13. Find and select **Order Record Assistant**
14. Click **Add**
15. A prompt may appear about related components - click **Add required objects**

### Part E: Verify All Components Are Present

16. Review your solution - it should contain:
    - Canvas App: Order Management App
    - Chatbot/Agent: Order Record Assistant
    - Cloud Flow: Create Order Flow
    - Table: Orders

17. Take a screenshot of the solution components list

### Part F: Publish All Customizations

18. Click **Publish all customizations** in the top menu bar
19. Wait for publishing to complete

### Part G: Export as Unmanaged Solution

20. Click **Export solution** in the top menu bar
21. In the export dialog:
    - Click **Next** on the first screen (publish options)
    - **Export type**: Select **Unmanaged**
    - **Version**: Keep as `1.0.0.0` or increment to `1.0.0.1`
22. Click **Export**
23. The file downloads as a `.zip` file named something like `OrderManagementSolution_1_0_0_0.zip`
24. Save this `.zip` file - this is your primary submission artifact

---

## Submission Preparation

### Folder structure to create

```
SubmissionFolder/
|-- OrderManagementSolution_1_0_0_0.zip   (exported unmanaged solution)
`-- Screenshots.pdf                         (all required screenshots)
```

### Required Screenshots in the PDF

Label each screenshot clearly with the name below:

**App Interface**
1. `Welcome Screen` - WelcomeScreen with image, greeting with your name, button
2. `Browse Screen` - BrowseScreen showing the back icon
3. `Create New Record Form` - EditScreen opened via the + icon (blank form)
4. `Edit Existing Record Form` - EditScreen opened via selecting an existing record
5. `Search Functionality` - BrowseScreen with text typed in the search box
6. `Copilot Agent Integration` - Copilot component or agent panel in the app
7. `Copilot Agent Conversation` - Full dialogue with the agent
8. `New Record Creation via Copilot` - New record visible in the app after creation

**Configuration and Logic**
9. `Solution Components` - The solution view showing app + agent + flow + table
10. `Power FX Navigate Function` - Formula bar showing `Navigate(BrowseScreen1, ScreenTransition.Fade)`
11. `Power Automate Flow Trigger` - Agent trigger block with all 4 parameters visible
12. `Dataverse Add New Row Action` - The Dataverse action with mapped fields
13. `Response Action` - The Respond to agent action showing the Product Name in the response
14. `Topic Trigger` - Copilot Studio topic trigger with trigger phrases visible
15. `Message Node` - The Send a message node showing the flow response variable
16. `Dataverse Table` - The table view showing data rows and table properties

### Final submission
- Compress the SubmissionFolder into a single `.zip` file
- Upload the `.zip` to Udacity

---

## Troubleshooting Reference

| Issue | Solution |
|---|---|
| Agent flow not visible in Copilot Studio | Make sure the flow was saved and is in the same environment |
| Dataverse table not found in flow | Confirm environment matches; re-select the table in the Dataverse action |
| User().FullName shows blank | Preview mode may not resolve user - test by publishing and running the app |
| Agent trigger phrases not firing | Check phrases for typos; ensure topic is set to active |
| Records not appearing after Copilot creates them | Refresh the app (close and reopen) or add a Refresh() call in the app |
| Export missing components | Use "Add required objects" when adding each component to the solution |
