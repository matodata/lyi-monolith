# lyi-monolith

## Requirement

### Two major requirements
- Inventory management
  - To track the inventory of various SKUs across distributors and outlets at any given point in time.
  - Generate reports on a daily and on-demand basis to understand how many SKUs are available with a given distributor and the outlets.
  - Ability to Create-Read-Update-Delete SKUs.
  - Ability to Increment-Decrement the stock units for a given SKU.
- Employee tracking
  - To track the employees attendance on how many outlets they visited on a specific day. Specifically ASMs.
  - To track whether they reached the outlet (geo-fencing) when they marked their attendance.
### Users of the app
- Admin.
  - Having god mode permission to edit any SKUs of any outlets/distributors. Used for correcting wrong submission.
  - Ability to onboard users with specific roles and permissions.
  - Ability to remove users when they leave the organization.
  - Ability to view reports generated.
  - Ability to map RSM with Distributors
  - Ability to map ASM with outlets.
- Management
  - Ability to generate reports for different SKUs across distributors and outlets pan-india. To start with, we just need to showcase in an excel format of how many units are with whom for a given SKU. (Report format draft)
  - Ability to view the attendance report of the ASM employees. (Report format draft)
- Regional Sales Manager (RSM)
  - Ability to generate reports specific to their distributors and outlets related to those distributors. (Report format draft)
Distributors
  - Ability to increment and decrement SKUs which are currently with them.
- Area Sales Manager (ASM)
  - Ability to increment and decrement SKUs on-behalf of the outlets they are assigned to.
  - Ability to view the list of outlets assigned to them along with their location on the app.
  - Ability to mark attendance at each outlet (Geo-fenced up to nearby X meters) when they visit them
