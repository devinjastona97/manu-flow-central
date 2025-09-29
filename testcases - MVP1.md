# MRP Platform Testing Acceptance Criteria

This document outlines the testing acceptance criteria for the Manufacturing Resource Planning (MRP) platform, covering all core modules with positive and negative test scenarios.

## Authentication Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Authentication | User login with valid credentials | A user with valid credentials exists in the system | User enters correct email and password | User is authenticated and redirected to dashboard |
| Authentication | User login with invalid credentials | A user attempts to login | User enters incorrect email or password | Error message is displayed and user remains on login page |
| Authentication | User logout | A user is logged into the system | User clicks logout button | User session is terminated and redirected to login page |
| Authentication | Session expiration | A user session has expired | User attempts to access protected route | User is redirected to login page with session expired message |

## Dashboard Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Dashboard | Display number of created products | The system has product records | User opens the dashboard | The widget displays the total number of created products |
| Dashboard | Display number of RFQs | The system has RFQ records | User opens the dashboard | The widget displays the total number of RFQs |
| Dashboard | Display number of Quotes | The system has Quote records | User opens the dashboard | The widget displays the total number of Quotes |
| Dashboard | Display number of Orders | The system has Order records | User opens the dashboard | The widget displays the total number of Orders |
| Dashboard | Display number of Invoices | The system has Invoice records | User opens the dashboard | The widget displays the total number of Invoices |
| Dashboard | Handle no data scenario | No data exists for products, RFQs, Quotes, Orders, or Invoices | User opens the dashboard | The corresponding widget displays 0 |
| Dashboard | Auto-refresh data | System has new records added | User refreshes the page or triggers refresh | Widgets update and reflect the latest counts |
| Dashboard | Unauthorized access | A user without permission to view dashboard | User attempts to open dashboard | User is redirected to login page or shown an “Access Denied” message |
| Dashboard | System error on data fetch | The system fails to fetch data from backend | User opens the dashboard | Widgets display “Data not available” with error state instead of crashing |

## User Management Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| User Group | Show list of user groups | User groups exist in the system | User opens the User Group List page | System displays all existing user groups with details (group name, description, member count, permissions) |
| User Group | Show empty user group list | No user groups exist | User opens the User Group List page | System displays “No groups available” |
| User Group | Show user group details | A group exists with assigned members and permissions | User clicks on a group | System displays group details (name, description, members, permissions) |
| User Group | Search by group name | User groups exist in the system | User enters a keyword in the search/filter field | System displays only groups that match the keyword |
| User Group | No matching search result | No group matches the entered keyword | User performs search | System displays “No results found” |
| User Group | Create user group | User has permission to manage groups | User enters valid group name and details | New group is created and appears in the group list |
| User Group | Create user group with missing/invalid data | User has permission to manage groups | User leaves required fields blank or enters invalid data | Validation message is shown and group is not created |
| User Group | Edit group information | A group exists | User updates group name or description | Group information is saved and updated in the list |
| User Group | Show list of members per group | A group has assigned members | User views group details | System displays all members in the group |
| User Group | Add member to group | A group exists and valid user exists | User selects and adds a user to the group | Member is added and appears in group member list |
| User Group | Delete member from group | Group has at least one member | User deletes a member from group | Member is removed from list |
| User Group | Manage permissions per member | A user exists in the system | User selects permissions for menus and actions | System saves permissions |
| User Group | Delete user group | Group exists and user has permission | User deletes the group | Group is removed from list (and associations handled as per system rules) |
| User Group | Delete user group with members | Group has members | User deletes the group | System either prompts confirmation (“Deleting this group will remove members' access”) |
| User Group | Unauthorized access | User lacks permission to manage groups | User tries to access User Group features | System denies access and shows “Access Denied” message |

## FX Management Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Currency | Set base currency | Admin is configuring system | Admin selects base currency for operations | System updates the base currency and applies it across transactions/products |
| Currency | Show list of all currencies | Currencies exist in the system | User opens Currency List page | System displays all currencies with details (code, name, status) |
| Currency | Show empty currency list | No currencies exist | User opens Currency List page | System shows “No currencies available” |
| Currency | Manage active/inactive status of Currency | A currency exists | Admin updates currency status | Currency is updated to Active/Inactive and reflected immediately |
| Currency | Add new valid currency | User has permission | Admin enters valid currency details | New currency is added and appears in the list |
| Currency | Prevent duplicate currency | A currency with the same code already exists | Admin tries to add it again | System prevents duplication and shows error message |
| Currency | Add new exchange rate with effective date | Currency exists | Admin enters rate and effective date | System saves the new rate and applies it from effective date onward |
| Currency | Prevent missing effective date | Admin adds exchange rate | Admin omits effective date | System shows validation error and prevents save |
| Currency | Show exchange rate history | Exchange rates exist | User opens exchange rate history | System displays full history sorted by date |
| Currency | Show empty exchange rate history | No exchange rates exist | User opens exchange rate history | System shows “No exchange rate history available” |

## Company Info Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Company Info | Edit company information (name, phone, email, address, logo) | Company profile exists | Admin updates company info fields | System saves the new info and updates across the system (including on generated documents) |
| Company Info | Upload/Update company logo | Admin has a valid image file | Admin uploads or replaces logo | Logo is updated and reflected across the system |
| Company Info | Prevent invalid logo upload | Admin uploads unsupported file format or exceeds size limit | Upload attempt is made | System shows error and does not update logo |
| Company Info | Show list of bank info | Bank info records exist | User opens Bank Info page | System displays all bank accounts with details (bank name, account holder, currency, account number, status) |
| Company Info | Show empty bank info list | No bank info exists | User opens Bank Info page | System shows “No bank info available” |
| Company Info | Create bank info | Admin enters valid bank account details | Admin saves new record | Bank info is added to the list and available for transactions |
| Company Info | Prevent duplicate bank info | A bank account with same details exists | Admin tries to add it again | System prevents duplication and shows validation error |
| Company Info | Edit bank info | Bank info exists | Admin updates bank details | System saves changes and updates the list |
| Company Info | Delete bank info | Bank info exists | Admin deletes a record | Bank info is removed from the list |
| Company Info | Prevent deletion of default bank account | A bank account is set as default | Admin attempts to delete it | System prevents deletion and shows warning (or requires selecting another default first) |
| Company Info | Set default bank info | Multiple bank accounts exist | Admin sets one account as default | System marks it as primary and uses it for transactions automatically |

## Inventory Module - Materials (Include Batch & Stock Movement)

### Materials

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Materials | Show list of all materials | Materials exist in the system | User opens Materials List page | System displays all raw materials and stock items with details |
| Materials | Show empty materials list | No materials exist | User opens Materials List page | System shows “No materials available” |
| Materials | Filter/Search by name | Materials exist with various names | User enters search keyword | System displays materials matching the keyword |
| Materials | Filter/Search by category | Materials exist in different categories | User applies category filter | System displays only materials in the selected category |
| Materials | Filter/Search by classification (ABC) | Materials exist with A/B/C classification | User applies classification filter | System displays only materials in that class |
| Materials | Filter/Search by type | Materials exist with multiple types (raw, semi-finished, consumable, spare part, service) | User applies type filter | System displays only materials of that type |
| Materials | Filter/Search by stockable/non-stockable | Materials exist with stockable and non-stockable status | User applies filter | System displays only materials matching the filter |
| Materials | Add new material with valid data | User is on materials management page and has permission | Admin enters required fields (SKU auto-generated, name, category, type, classification, UOM, stockable setting, status) | Material is created and appears in list |
| Materials | Add new category during material creation | User is creating a material | Admin selects “Add New Category” option | System allows creating new category and assigning it to material |
| Materials | Add new UOM during material creation | User is creating a material | Admin selects “Add New UOM” option | System allows creating new UOM and assigning it to material |
| Materials | Prevent duplicate material | Material with same name/SKU already exists | Admin tries to add it again | System prevents duplication and shows validation error |
| Materials | Update material details | Material exists | Admin edits material info (category, type, UOM, status, etc.) | System saves updates and reflects in list |
| Materials | Bulk upload valid materials | User has permission and valid file format | Admin uploads file with multiple materials | System processes file and adds materials to list |
| Materials | Prevent bulk upload errors | File has missing/invalid fields | Admin uploads file | System rejects invalid records, shows error log, and only valid records are created |

### Material Category Management

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Material Category Management | Show all categories | Categories exist | User opens Category Management tab | System displays all created categories (Name, Alias, Status) |
| Material Category Management | Show empty list | No categories exist | User opens Category Management tab | System displays “No categories available” |
| Material Category Management | Create valid category | User has permission | User enters category name and alias, then saves | System creates a new category, displays it in the list, and sets it Active by default |
| Material Category Management | Prevent duplicate | A category with the same name exists | User tries to add duplicate | System rejects the entry and shows “Category already exists” |
| Material Category Management | Update existing category | Category exists | User edits name or alias | System saves changes and updates the list |
| Material Category Management | Manage status, Toggle on/off | Category exists | User changes status to inactive | System marks category as inactive and excludes it from dropdowns in material creation |

### Material UOM Management

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Material UOM Management | Show all UOMs | UOMs exist | User opens UOM Management tab | System displays all created UOMs (Name, Alias, Status) |
| Material UOM Management | Show empty list | No UOMs exist | User opens UOM Management tab | System displays “No UOMs available” |
| Material UOM Management | Create valid UOM | User has permission | User enters UOM name and alias, then saves | System creates a new UOM, displays it in the list, and sets it Active by default |
| Material UOM Management | Prevent duplicate | A UOM with the same name exists | User tries to add duplicate | System rejects the entry and shows “UOM already exists” |
| Material UOM Management | Update existing UOM | UOM exists | User edits name or alias | System saves changes and updates the list |
| Material UOM Management | Manage status, Toggle on/off | UOM exists | User changes status to inactive | System marks UOM as inactive and excludes it from dropdowns in material creation |

### Material - Batches

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Material - Batches | Show list of all created batches on specific material | Batches exist | User opens Batch List tab on Material Detail page | System displays all batches (Batch ID, Material, Qty, Vendor, Cost, Expiry, Storage Location, Status) |
| Material - Batches | Show empty batch list | No batches exist | User opens Batch List page | System shows “No batches available” |
| Material - Batches | Filter/Search by keyword | Batches exist | User enters search keyword (Batch ID or Material) | System displays only matching batches |
| Material - Batches | Filter/Search by status | Batches exist with multiple statuses | User applies status filter | System displays batches with that status |
| Material - Batches | Filter/Search by vendor | Batches exist from multiple vendors | User applies vendor filter | System displays batches from selected vendor |
| Material - Batches | Filter/Search by storage location | Batches exist in multiple locations | User applies location filter | System displays batches from selected storage |
| Material - Batches | Filter/Search by expiry | Batches exist with expiry dates | User applies filter “Expired” or “Non-expired” | System displays batches accordingly |
| Material - Batches | Toggle empty batches | Some batches have zero quantity | User enables “Show Empty Batches” toggle | System includes empty batches in the list |
| Material - Batches | Create new batch with details | User has permission | Admin enters material, quantity, cost, vendor, expiry (optional), storage location | System auto-generates Batch ID, assigns status = Received, saves the batch |
| Material - Batches | Update batch details | Batch exists | Admin edits cost, storage, expiry, or status | System saves updates and reflects changes |
| Material - Batches | Adjust batch quantity | Batch exists | Admin adjusts Current Quantity manually | System updates batch quantity, total material stock is recalculated |
| Material - Batches | Prevent deleting batch with stock | Batch exists and quantity > 0 and status = Received | Admin tries to delete batch | System blocks deletion |
| Material - Batches | Allow deleting empty batch | Batch exists and quantity = 0 or status != Received | Admin deletes batch | System removes batch from system |
| Material - Batches | Material stock total | Multiple batches exist with different statuses | System calculates total stock for material | Only batches with status = Received are included in material’s total available stock |

### Stock Movement

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Stock Movement | Show all transactions for that material | Stock movements exist | User opens Stock Movement tab | System shows all related movements (Date, Movement Type, Batch ID, Qty, Work Order, Product) |
| Stock Movement | Show empty state | No stock movements exist for the material | User opens Stock Movement tab | System shows “No stock movements available” |
| Stock Movement | Filter by date | Movements exist on multiple dates | User applies a date range filter | System displays only movements in that date range |
| Stock Movement | Filter by type | Movements include in, out, adjustment | User applies type filter | System shows only those movement types |
| Stock Movement | Filter by batch | Movements are linked to multiple batches | User applies batch filter | System shows only movements from that batch |
| Stock Movement | Filter by work order / product | Movements are tied to work orders/products | User applies work order filter | System shows only relevant transactions |
| Stock Movement | Auto logging | A system transaction occurs | System processes transaction | System automatically adds the movement to this tab with Transaction ID, Date, User, and Remarks |
| Stock Movement | Deduct stock using FIFO | Material is issued for usage/production | System checks all batches with status = Received | Stock is deducted starting from the oldest batch first (FIFO) |
| Stock Movement | Expired batch handling | Batch has expired date and current date > expiry | System checks batch status | Batch is marked Expired and excluded from available stock |
| Stock Movement | History cannot be altered | Stock movements already logged | User views Stock Movement tab | Records are read-only; no edits or deletes allowed |

## Products Management Module

### Product

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Product | Show all products with details (SKU, Name, Category, Status) | Products exist | User opens Product List page | System displays all created products with their details |
| Product | Show empty product list | No products exist | User opens Product List page | System displays “No products available” |
| Product | Search by product name | Products exist with different names | User searches by name | System displays only products matching the keyword |
| Product | Filter by category | Products exist in multiple categories | User applies category filter | System displays products in the selected category |
| Product | Filter by status (active/inactive) | Products exist with active/inactive status | User applies status filter | System shows only products matching the selected status |
| Product | Add product with valid details (SKU, Name, Category, Images, BOM, Lead Time, Base & Selling Price) | User has permission | User enters all required details | System creates the product and displays it in the product list |
| Product | Prevent duplicate product creation | Product with same name already exists | User tries to create the same product again | System blocks creation and shows “Product already exists” |
| Product | Ensure selling price consistency (≥ base price) | User creates/edits a product | User enters a selling price lower than base price | System blocks save and shows “Selling price must be ≥ base price” |
| Product | Upload product image | User has permission | User uploads an image during product creation/edit | System attaches the image to the product and shows preview |
| Product | Replace product image | Product exists with an image | User uploads a new image | System replaces the existing image with the new one |
| Product | Delete product image | Product exists with an image | User removes the image | System deletes the image and updates product record |
| Product | Edit product details (Name, Category, BOM, Pricing, Images, Lead Time) | Product exists | User edits product details | System updates the product details |
| Product | Deactivate product (status change) | Product exists | User deactivates the product | System marks product inactive and excludes it from selection in sales/production |
| Product | Reactivate product | Product exists but inactive | User reactivates the product | System sets product to active and includes it again in dropdowns |
| Product | Assign BOM to product | BOMs exist in system | User selects BOM for product | System links product to the chosen BOM |
| Products | Delete product not referenced in orders | A product exists without order references | User deletes the product | Product is removed from system successfully |
| Products | Delete product referenced in orders | A product exists with active order references | User attempts to delete the product | Error message prevents deletion due to existing references |
| Products | Bulk upload products with valid CSV | User has valid CSV file with product data | User uploads CSV file through bulk upload | All valid products are imported successfully |
| Products | Bulk upload with invalid CSV format | User has malformed CSV file | User attempts to upload invalid CSV | Error message details formatting issues |

### Product Category Management

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Product Category Management | Show all categories | Categories exist | User opens Category Management tab on Product Page | System displays a list of all created categories (Name, Alias, Status) |
| Product Category Management | Show empty list | No categories exist | User opens Category Management tab on Product Page | System displays “No categories available” |
| Product Category Management | Create valid category | User has permission | User enters category name and alias, then saves | System creates a new category, displays it in the list, and sets it Active by default |
| Product Category Management | Prevent duplicate | A category with the same name exists | User tries to add duplicate | System rejects the entry and shows “Category already exists” |
| Product Category Management | Update existing category | Category exists | User edits name or alias | System saves changes and updates the list |

## Manufacturing Module (Recipes, BOM, Routing)

### Routing

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Routing | Show all created routings in a list (with name, description, created date, status) | Routings exist | User opens Routing List page | System displays all created routings with details |
| Routing | Show empty routing list | No routings exist | User opens Routing List page | System displays “No routings available” |
| Routing | Add new routing | User has permission | User clicks Add Routing, enters valid details (name, description, stages) | System creates the routing and displays it in the list |
| Routing | Prevent duplicate routing name | Routing with the same name already exists | User tries to create routing with the same name | System blocks creation and shows “Routing already exists” |
| Routing | Edit routing details (name, description, stages) | Routing exists | User clicks Edit Routing, updates info | System updates routing details |
| Routing | Deactivate routing | Routing exists and active | User sets routing to inactive | System marks routing as inactive, keeps it valid for existing BOMs, but hides it from selection in new BOM creation or editing |
| Routing | Reactivate routing | Routing exists but inactive | User sets routing to active | System marks routing as active and makes it selectable again for BOM creation and editing |

### BOM

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| BOM | Displays list of all created BOMs | BOMs exist | User opens BOM List page | System shows all BOMs with columns (BOM Name, Product, Recipe Name, Status) |
| BOM | Show empty BOM list | No BOMs exist | User opens BOM List page | System displays “No BOMs available” |
| BOM | Search/filter BOMs by BOM name | BOMs exist with different names | User searches by BOM name | System displays only BOMs matching the keyword |
| BOM | Filter BOMs by product | BOMs exist for multiple products | User applies product filter | System shows only BOMs for the selected product |
| BOM | Filter BOMs by recipe name | BOMs exist with different recipe names | User applies recipe name filter | System shows only BOMs for that recipe |
| BOM | Filter BOMs by status | BOMs exist with active/inactive status | User applies status filter | System shows only BOMs matching the chosen status |
| BOM | Create new BOM | User has permission | User clicks Create BOM, enters product, recipe name, description | System creates the BOM and shows it in the list |
| BOM | Prevent duplicate BOM | A BOM for the same product and recipe exists | User tries to create another with same product and recipe | System blocks creation and shows “BOM already exists” |
| BOM | Add material to BOM | BOM exists | User selects material and defines usage quantity | System adds material to BOM with specified quantity |
| BOM | Delete material from BOM | BOM has materials assigned | User deletes a material from the BOM | System removes the material and updates BOM composition |
| BOM | Manage routing stages | Routing exists | User selects routing stages for the BOM | System links the routing stages to the BOM |
| BOM | Edit BOM | BOM exists | User updates materials, routing, or description | System saves changes and updates BOM |
| BOM | Deactivate BOM | BOM exists and active | User sets BOM to inactive | System marks BOM as inactive, keeps it valid for historical data, but prevents it from being used in new production orders |
| BOM | Reactivate BOM | BOM exists but inactive | User sets BOM to active | System marks BOM as active and allows it to be used again in production |
| BOM | Validation: BOM must have at least one material | User is creating BOM | User tries to save BOM without materials | System blocks save and shows “BOM must have at least one material” |
| BOM | Validation: BOM must have at least one routing stage | User is creating BOM | User tries to activate BOM without routing | System blocks activation and shows “BOM must have at least one routing stage” |
| BOM | Calculate recipe total cost | A recipe exists with materials and personnel | System calculates recipe costs | Total cost is computed from all recipe components |

## Sales Management Module (RFQs, Quotes)

### RFQ

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| RFQ | Show all created RFQs | RFQs exist | User opens RFQ List page | System displays all created RFQs with details (RFQ ID, Customer, Status, Requested By, Approval Info) |
| RFQ | Show empty RFQ list | No RFQs exist | User opens RFQ List page | System shows “No RFQs available” |
| RFQ | Search / Filter RFQ by customer or ID | Multiple RFQs exist | User applies filter by customer or RFQ ID | System shows only RFQs matching the filter |
| RFQ | View RFQ Details | RFQ exists | User clicks View on RFQ list | System displays RFQ details: Customer Info, Target Completion, Products, Notes, Attachments, Status, Approval history |
| RFQ | Save as Draft | User fills RFQ form (all mandatory fields are filled) | User clicks Save Draft | RFQ is saved in Draft status and shown in RFQ list |
| RFQ | Add Product(s) to RFQ (mandatory qty) | Product(s) exist in product master | User selects product, enters quantity (mandatory), adds optional notes/documents, clicks Add Product | Product(s) are linked to the RFQ and displayed in RFQ’s Products section |
| RFQ | Submit RFQ (validations) | Draft exists and all mandatory fields are filled | User clicks Submit | RFQ status updates to Submitted (waiting for approval), and system records |
| RFQ | Update Draft | RFQ in Draft status | User edits customer info, products, notes | System updates RFQ details |
| RFQ | Restrict edit after submit | RFQ in Submitted/Approved/Rejected status | User tries to edit | System blocks edits and shows message: “RFQ can only be edited in Draft status” |
| RFQ | Approve RFQ | RFQ in Submitted status | Approver clicks Approve | System updates RFQ status to Approved and records |
| RFQ | Reject RFQ | RFQ in Submitted status | Approver clicks Reject | System updates RFQ status to Rejected |
| RFQ | Convert Approved RFQ to Quotation | RFQ status is Approved | System auto-generates linked Quotation | Quotation inherits products, customer, and notes from RFQ |

### Quote

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Quote | Show all created Quotes | Quotes exist | User opens Quote List page | System displays all created Quotes with details (Quote ID, Customer, Status, Requested By, Approval Info) |
| Quote | Show empty Quote list | No Quotes exist | User opens Quote List page | System shows “No Quotes available” |
| Quote | Search / Filter Quotes by customer or ID | Multiple Quotes exist | User applies filter by customer or Quote ID | System shows only Quotes matching the filter |
| Quote | View Quote Details | Quote exists | User clicks View on Quote list | System displays Quote details: Customer Info, Products, Fees/Tax/Discounts, Terms, Attachments, Status, Approval history |
| Quote | Save as Draft | User fills Quote form (all mandatory fields are filled) | User clicks Save Draft | Quote is saved in Draft status and shown in Quote list |
| Quote | Create Quote (validations) | All mandatory fields provided | User clicks Submit | Quote status updates to Submitted (waiting for internal approval), and system records Requested by [user] and timestamp |
| Quote | Add Products | Quote creation form is open | User clicks Add Product and selects products with qty & unit price | System adds products to Quote and calculates Subtotal |
| Quote | Calculate Total Amount | Products are added to Quote | User enters Tax Rate, Shipping Fee, Other Fee | System auto-calculates Tax Total and Total |
| Quote | Edit Quote (Draft only) | Quote in Draft status | User edits customer info, products, pricing, terms | System updates Quote details |
| Quote | Restrict edit after submit | Quote in Submitted/Approved/Rejected status | User tries to edit | System blocks edits and shows message: “Quote can only be edited in Draft status” |
| Quote | Internal Approval | Quote in Submitted status | Manager/Approver clicks Approve | System updates status to Issued (internally approved & sent to customer) and records Approved by/timestamp |
| Quote | Internal Rejection | Quote in Submitted status | Manager/Approver clicks Reject | System updates status to Rejected (Internal) and records rejection reason |
| Quote | Internal Revision Request | Quote in Submitted status | Approver requests revision | System updates status to Need Revision (Internal) and notifies the sales team |
| Quote | Customer Pending Status | Quote is Issued | Quote sent to customer | System shows status Pending (waiting for customer decision) |
| Quote | Customer Approval | Quote is Issued | Customer clicks Approve | Quote status updates to Approved (Customer), auto-generates Order, and DP Invoice if applicable |
| Quote | Customer Reject | Quote is Issued | Customer clicks Reject | Quote status updates to Rejected (Customer) |
| Quote | Customer Requests Revision | Quote is Issued | Customer requests changes | System updates status to Need Revision (Customer) and notifies sales team |
| Quote | Auto-generate Order from Approved Quote | Quote status is Approved (Customer) | System processes | Linked Order created with inherited products, customer, fees, tax, and terms |
| Quote | Auto-generate Down Payment Invoice | Quote includes DP and is Approved | System processes | DP Invoice generated reflecting DP %/amount |
| Quote | Download Quote as PDF | Quote exists | User clicks Download PDF | System generates and downloads a PDF version of the Quote |

## Orders Management Module (Include Shipment)

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Order | Show all created Orders | Orders exist | User opens Order List page | System displays all Orders with details (Order ID, Customer, Linked Quote, Status, Progress, Approval Info) |
| Order | Show empty Order list | No Orders exist | User opens Order List page | System shows “No Orders available” |
| Order | Search / Filter Orders | Multiple Orders exist | User applies filter by customer, Order ID, or status | System shows only Orders matching the filter |
| Order | View Order Details | Order exists | User clicks View on Order list | System displays details: Linked Quotation, Products, Work Orders, Invoices, Shipments, Attachments, Progress, Approval history |
| Order | Submit for Approval | Order created (Not Started) and DP paid | User clicks Submit for Approval | Order status updates to Waiting for Approval and workflow starts |
| Order | Approve Order | Order in Waiting for Approval | Approver clicks Approve | Order status updates to Confirmed, system locks Order, and auto-generates Work Orders per product |
| Order | Reject Order | Order in Waiting for Approval | Approver clicks Reject | Order status updates to Canceled |
| Order | Change Order Status (system-driven) | Order exists | Order progresses | System updates status through lifecycle: Not Started → Waiting for Approval → Confirmed → In Progress → Completed → Closed → Canceled |
| Order | Trigger Production Start | Order status = Confirmed | System triggers production | System automatically creates linked Work Orders per ordered product |
| Order | Manage Attachments (SPK) | Order exists | User uploads SPK/documents | Documents stored and linked to Order |
| Order | Manage Shipping Documents | Order exists | User uploads shipment-related docs | Docs stored, organized in tabs, marked completed/incomplete based on Incoterms |
| Order | Track Work Order Progress | Order linked to Work Orders | User views Order details | System shows per-product WO progress (% completion, status updates) |
| Order | View Linked Invoice | Order invoiced | User views Order details | System shows linked Invoice(s), including DP invoice if applicable |
| Order | Track Shipment | Order shipped | User views Order details | System shows linked Shipment status and uploaded documents |
| Order | Mark order as shipped | Order ready for shipping | User marks order as shipped | Order status updates and customer notified |
| Order | Auto-close | Order execution and financials completed | System detects WO completed + Invoice settled | System updates Order status to Closed |

## Work Order Management Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Work Order | Show all Work Orders | Work Orders exist | User opens Work Order List page | System displays all active and completed Work Orders with details (WO ID, Linked Order, Product, Quantity, Status, Start Date, End Date, Progress) |
| Work Order | Show empty Work Order list | No Work Orders exist | User opens Work Order List page | System shows “No Work Orders available” |
| Work Order | Search / Filter Work Orders | Multiple Work Orders exist | User applies filter by product, status, linked Order, or date | System shows only Work Orders matching the filter |
| Work Order | Auto-generate from Order | Order is approved and status = Confirmed | System auto-generates Work Orders per product | Work Orders are created with details: Product, Quantity, Linked BOM, Routing, and linked back to the Order |
| Work Order | View Work Order Details | Work Order exists | User clicks View on Work Order list | System displays details: Linked Order, Product, Quantity, BOM, Routing, Required Materials, Attachments, Progress updates |
| Work Order | Track Production Progress | Work Order exists | User updates or views production steps | System records actual progress per step (start, in-progress, completed) and updates overall status (% completion) |
| Work Order | Manage Materials (usage) | Work Order has linked BOM | User records material usage | System deducts used materials from inventory and logs actual vs planned consumption |
| Work Order | Add Attachments | Work Order exists | User uploads files (design files, production instructions, QC checklist) | Files are stored and linked to the Work Order |
| Work Order | Change Work Order Status | Work Order exists | Work Order progresses through lifecycle | System updates status as: Ready to Process → In Progress → Completed → Canceled |
| Work Order | Complete Work Order | Work Order tasks finished | User marks Complete | System updates status to Completed, triggers stock updates, and notifies linked Order |
| Work Order | Auto-completed | Work Order completed and Order is completed | System detects no pending tasks | System auto-updates Work Order status to Completed |

## Invoicing Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Invoice | Show all Invoices | Invoices exist | User opens Invoice List page | System displays all created Invoices with details (Invoice ID, Linked Order, Customer, Amount, Due Date, Status, Payment Info) |
| Invoice | Show empty Invoice list | No Invoices exist | User opens Invoice List page | System shows “No Invoices available” |
| Invoice | Search / Filter Invoices | Multiple Invoices exist | User applies filter by customer, order, status, or date | System shows only Invoices matching the filter |
| Invoice | Create Invoice | Order exists and ready for invoicing | User creates Invoice linked to Order, sets due date, and saves | System generates Invoice with status Issued, linked to the Order, and displays in Invoice list |
| Invoice | View Invoice Details | Invoice exists | User clicks View on Invoice list | System displays details: Linked Order, Customer, Amount, Due Date, Status, Payment Notes, and Documents |
| Invoice | Mark invoice as paid | An unpaid invoice exists | User marks invoice as paid | Invoice status changes to Paid and payment date is recorded |
| Invoice | Manage Invoice Status | Invoice exists | User changes Invoice status (Issued, Paid, Void, Cancelled) | System updates status and records history of changes |
| Invoice | Download/Export Invoice PDF | Invoice exists | User clicks Download/Export PDF | System generates and downloads PDF version |
| Invoice | View invoice payment history | A paid invoice exists | User views invoice details | Payment history and dates are displayed |

## Customer Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Customer | Show all Customers | Customers exist | User opens Customer List page | System displays all Customers with details (Customer ID, Name, Company, PIC Name, Contact Info, Status) |
| Customer | Show empty Customer list | No Customers exist | User opens Customer List page | System shows “No Customers available” |
| Customer | Search / Filter Customers | Multiple Customers exist | User applies filter by name, email, phone, or status | System shows only Customers matching the filter |
| Customer | Create Customer Profile | System ready to store customer data | User enters customer details (name, company, PIC info, contacts) and saves | System creates Customer profile, assigns unique ID, and displays in Customer list |
| Customer | View Customer Details | Customer exists | User clicks View on Customer list | System displays details: Name, Company, Contact Info, PIC Name, PIC Phone, PIC Email, Status |
| Customer | Edit Customer Details | Customer exists | User edits customer details and saves | System updates profile with new information |
| Customer | Activate Customer | Customer status = Inactive | User sets status to Active | System updates customer status to Active, making it available for use in Orders/Invoices |
| Customer | Deactivate Customer | Customer status = Active | User sets status to Inactive | System updates customer status to Inactive, preventing new Orders/Invoices but retaining historical records |

## Reporting & Analytics Module

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Reporting | Show Finance Reports | Finance data (Orders, Invoices) exist | User selects Finance Reports | System displays: Total Revenue, Monthly Revenue, Total Orders, Paid vs Unpaid Invoices, Top 10 Products by Value, Top 10 Products by Quantity Sold, Top Customers by Revenue |
| Reporting | Show Inventory Reports | Inventory transactions exist | User selects Inventory Reports | System displays: Fast Moving Materials, ABC Inventory Classification, Inventory Value |
| Reporting | Show Order Reports | Orders and Work Orders exist | User selects Order Reports | System displays: Orders by status (To-do, Ongoing, Done), Work Orders by status (To-do, Ongoing, Done), Ongoing Time Count for Orders |
| Reporting | Show Sales Funnel Reports | RFQ, Quote, and Order data exist | User selects Sales Funnel Reports | System displays: RFQ Distribution, Total RFQ, Conversion Rate, Avg Days RFQ → Quote, Avg Days Quote → Order, Avg Days Order → Completion |
| Reporting | Show empty report (no data) | No data exists for selected report | User opens a report section | System shows “No data available” |
| Reporting | Apply Filters (all reports) | Data exists | User applies filters (date range, product, customer, etc.) | System shows report recalculated with applied filters |
| Reporting | Export Reports | Report is generated | User clicks Export (PDF/Excel) | System exports and downloads report in selected format |


## Error Handling and Edge Cases

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| System | Handle database connection failure | System is operational | Database becomes unavailable | User sees appropriate error message and retry options |
| System | Handle large file uploads | User is uploading files | User uploads file exceeding size limits | Error message indicates file size restrictions |
| System | Handle concurrent user edits | Multiple users access same record | Users edit same record simultaneously | System prevents data conflicts with appropriate messaging |
| System | Handle session timeout | User session is active | User session expires during operation | User is redirected to login with session timeout message |
| System | Handle malformed data import | User is importing data | Import file contains invalid data format | System validates data and reports specific errors |
| System | Handle insufficient permissions | User has limited permissions | User attempts unauthorized action | Access denied message is displayed |
| Validation | Handle SQL injection attempts | User input fields exist | Malicious SQL is entered in form fields | Input is sanitized and prevents database compromise |
| Validation | Handle XSS attack attempts | User input accepts HTML | Malicious scripts are entered | Input is sanitized and scripts are neutralized |
| Performance | Handle large dataset queries | Large amounts of data exist | User queries extensive data sets | Results are paginated and loading states are shown |
| Performance | Handle slow network conditions | System is accessed over slow connection | User performs data-heavy operations | Loading indicators and progress bars are displayed |

## Integration Testing Scenarios

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Workflow | Complete RFQ to Invoice flow | Customer submits quote request | Full workflow from RFQ → Quote → Order → Invoice | All stages complete successfully with data consistency |
| Workflow | Recipe to Work Order integration | Recipe exists for product in work order | Work order is created for product with recipe | Recipe requirements are automatically populated |
| Workflow | Material allocation workflow | Work order requires materials | Materials are allocated and work order progresses | Stock levels update and allocations are tracked |
| Workflow | User permission inheritance | User is assigned to group with permissions | User attempts actions covered by group permissions | User can perform authorized actions within group scope |
| Data Sync | Cross-module data consistency | Data exists across multiple modules | Changes are made in one module | Related data in other modules reflects changes correctly |

## Performance and Load Testing

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Performance | Handle concurrent users | System supports multiple users | 50+ users access system simultaneously | System maintains responsiveness and data integrity |
| Performance | Large data set handling | System contains 10,000+ records | Users query and filter large datasets | Results load within acceptable time limits |
| Performance | File upload performance | System accepts file uploads | Large files (50MB+) are uploaded | Upload completes with progress indication |
| Performance | Report generation performance | Large amounts of historical data exist | Complex reports are generated | Reports generate within reasonable time limits |

## Security Testing

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Security | Unauthorized API access | API endpoints exist | Direct API calls are made without authentication | Access is denied with appropriate error codes |
| Security | Role-based access control | Users with different roles exist | User attempts to access restricted functionality | Access is granted or denied based on user role |
| Security | Data encryption | Sensitive data exists in system | Data is transmitted and stored | All sensitive data is properly encrypted |
| Security | Audit logging | User actions occur in system | Administrative actions are performed | Actions are logged with user, timestamp, and details |

## Browser Compatibility

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Compatibility | Chrome browser support | User accesses system via Chrome | User performs all standard operations | All functionality works correctly in Chrome |
| Compatibility | Firefox browser support | User accesses system via Firefox | User performs all standard operations | All functionality works correctly in Firefox |
| Compatibility | Safari browser support | User accesses system via Safari | User performs all standard operations | All functionality works correctly in Safari |
| Compatibility | Mobile browser support | User accesses system via mobile browser | User performs mobile-appropriate operations | Interface is responsive and functional on mobile |

## Data Backup and Recovery

| Module | Description | Given | When | Then |
|--------|-------------|-------|------|------|
| Backup | Automatic data backup | System is operational | Daily backup process runs | All system data is backed up successfully |
| Recovery | Data recovery from backup | System failure occurs | Data recovery is initiated from backup | System is restored with minimal data loss |
| Recovery | Point-in-time recovery | Specific recovery point is needed | Recovery to specific date/time is requested | System is restored to exact requested state |

---

*This document should be updated as new features are added or existing functionality is modified. Each test case should be executed during release testing to ensure system quality and reliability.*
