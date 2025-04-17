---
layout: default
title: Database Models
---

# LYI Monolith Database Models

This document describes the database entities (models) used in the LYI Monolith application.

## Table of Contents
- [User](#user)
- [Role](#role)
- [SKU](#sku)
- [Distributor](#distributor)
- [Outlet](#outlet)
- [DistributorInventory](#distributorinventory)
- [OutletInventory](#outletinventory)
- [InventoryTransaction](#inventorytransaction)
- [OutletAsmMapping](#outletasmmapping)
- [DistributorRsmMapping](#distributorrsmmapping)
- [Attendance](#attendance)

## User

The User entity represents the different users of the system.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| username | String | Unique username for login |
| password | String | Encrypted password |
| email | String | User's email address |
| firstName | String | User's first name |
| lastName | String | User's last name |
| phone | String | User's phone number |
| role | Role | User's role in the system |
| active | Boolean | Whether the user is active |
| createdAt | Timestamp | When the record was created |
| updatedAt | Timestamp | When the record was last updated |

### Relationships
- One-to-Many with `OutletAsmMapping` (for ASM users)
- One-to-Many with `DistributorRsmMapping` (for RSM users)
- One-to-Many with `Attendance` (for ASM users)

## Role

The Role entity represents the different roles in the system.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| name | String | Role name |
| description | String | Role description |

### Predefined Roles
- ADMIN
- MANAGEMENT
- RSM (Regional Sales Manager)
- ASM (Area Sales Manager)
- DISTRIBUTOR

## SKU

The SKU entity represents the stock keeping units in the system.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| name | String | Name of the SKU |
| description | String | Description of the SKU |
| category | String | Category of the SKU |
| price | Decimal | Price of the SKU |
| barcode | String | Barcode of the SKU |
| active | Boolean | Whether the SKU is active |
| createdAt | Timestamp | When the record was created |
| updatedAt | Timestamp | When the record was last updated |

### Relationships
- One-to-Many with `DistributorInventory`
- One-to-Many with `OutletInventory`
- One-to-Many with `InventoryTransaction`

## Distributor

The Distributor entity represents the distributors in the system.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| name | String | Name of the distributor |
| address | String | Address of the distributor |
| city | String | City of the distributor |
| state | String | State of the distributor |
| pincode | String | PIN code of the distributor |
| phone | String | Phone number of the distributor |
| email | String | Email address of the distributor |
| contactPerson | String | Name of the contact person |
| active | Boolean | Whether the distributor is active |
| createdAt | Timestamp | When the record was created |
| updatedAt | Timestamp | When the record was last updated |

### Relationships
- One-to-Many with `Outlet`
- One-to-Many with `DistributorInventory`
- One-to-Many with `DistributorRsmMapping`

## Outlet

The Outlet entity represents the retail outlets in the system.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| name | String | Name of the outlet |
| address | String | Address of the outlet |
| city | String | City of the outlet |
| state | String | State of the outlet |
| pincode | String | PIN code of the outlet |
| phone | String | Phone number of the outlet |
| latitude | Double | Latitude of the outlet location |
| longitude | Double | Longitude of the outlet location |
| distributor | Distributor | Distributor associated with the outlet |
| active | Boolean | Whether the outlet is active |
| createdAt | Timestamp | When the record was created |
| updatedAt | Timestamp | When the record was last updated |

### Relationships
- Many-to-One with `Distributor`
- One-to-Many with `OutletInventory`
- One-to-Many with `OutletAsmMapping`
- One-to-Many with `Attendance`

## DistributorInventory

The DistributorInventory entity represents the inventory of SKUs at a distributor.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| distributor | Distributor | The distributor |
| sku | SKU | The SKU |
| quantity | Integer | Quantity of the SKU |
| lastUpdated | Timestamp | When the inventory was last updated |
| updatedBy | User | User who last updated the inventory |

### Relationships
- Many-to-One with `Distributor`
- Many-to-One with `SKU`
- Many-to-One with `User` (updatedBy)

## OutletInventory

The OutletInventory entity represents the inventory of SKUs at an outlet.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| outlet | Outlet | The outlet |
| sku | SKU | The SKU |
| quantity | Integer | Quantity of the SKU |
| lastUpdated | Timestamp | When the inventory was last updated |
| updatedBy | User | User who last updated the inventory |

### Relationships
- Many-to-One with `Outlet`
- Many-to-One with `SKU`
- Many-to-One with `User` (updatedBy)

## InventoryTransaction

The InventoryTransaction entity represents transactions that modify inventory.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| sku | SKU | The SKU involved in the transaction |
| distributorId | UUID | ID of the distributor (if applicable) |
| outletId | UUID | ID of the outlet (if applicable) |
| quantity | Integer | Quantity change (positive for increment, negative for decrement) |
| transactionType | Enum | Type of transaction (INCREMENT, DECREMENT) |
| entityType | Enum | Type of entity (DISTRIBUTOR, OUTLET) |
| transactionTime | Timestamp | When the transaction occurred |
| performedBy | User | User who performed the transaction |
| notes | String | Additional notes about the transaction |

### Relationships
- Many-to-One with `SKU`
- Many-to-One with `User` (performedBy)

## OutletAsmMapping

The OutletAsmMapping entity represents the mapping between ASM users and outlets.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| outlet | Outlet | The outlet |
| asm | User | The ASM user |
| assignedDate | Timestamp | When the ASM was assigned to the outlet |
| assignedBy | User | User who assigned the ASM to the outlet |
| active | Boolean | Whether the mapping is active |

### Relationships
- Many-to-One with `Outlet`
- Many-to-One with `User` (asm)
- Many-to-One with `User` (assignedBy)

## DistributorRsmMapping

The DistributorRsmMapping entity represents the mapping between RSM users and distributors.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| distributor | Distributor | The distributor |
| rsm | User | The RSM user |
| assignedDate | Timestamp | When the RSM was assigned to the distributor |
| assignedBy | User | User who assigned the RSM to the distributor |
| active | Boolean | Whether the mapping is active |

### Relationships
- Many-to-One with `Distributor`
- Many-to-One with `User` (rsm)
- Many-to-One with `User` (assignedBy)

## Attendance

The Attendance entity represents the attendance of ASM users at outlets.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Primary key |
| outlet | Outlet | The outlet visited |
| user | User | The ASM user who visited the outlet |
| checkInTime | Timestamp | When the ASM checked in at the outlet |
| latitude | Double | Latitude of the check-in location |
| longitude | Double | Longitude of the check-in location |
| validLocation | Boolean | Whether the check-in location is valid (within geo-fence) |
| notes | String | Additional notes about the visit |

### Relationships
- Many-to-One with `Outlet`
- Many-to-One with `User` 