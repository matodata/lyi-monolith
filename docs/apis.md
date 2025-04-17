---
layout: default
title: API Documentation
---

# LYI Monolith API Documentation

This document outlines the RESTful API endpoints for the LYI Monolith application.

## Table of Contents
- [Authentication](#authentication)
- [SKU Management](#sku-management)
- [Inventory Management](#inventory-management)
- [User Management](#user-management)
- [Outlet Management](#outlet-management)
- [Distributor Management](#distributor-management)
- [Attendance Management](#attendance-management)
- [Reports](#reports)

## Authentication

### Login
- **URL**: `/api/auth/login`
- **Method**: `POST`
- **Description**: Authenticate a user and return a JWT token
- **Request Body**:
```json
{
  "username": "string",
  "password": "string"
}
```
- **Response**:
```json
{
  "token": "string",
  "userId": "string",
  "username": "string",
  "role": "string"
}
```

### Logout
- **URL**: `/api/auth/logout`
- **Method**: `POST`
- **Description**: Invalidate the user's session
- **Authorization**: Bearer Token
- **Response**: `204 No Content`

## SKU Management

### Create SKU
- **URL**: `/api/skus`
- **Method**: `POST`
- **Description**: Create a new SKU
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "name": "string",
  "description": "string",
  "category": "string",
  "price": "number",
  "barcode": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "category": "string",
  "price": "number",
  "barcode": "string",
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Get All SKUs
- **URL**: `/api/skus`
- **Method**: `GET`
- **Description**: Retrieve all SKUs
- **Authorization**: Bearer Token
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: name)
  - `direction`: Sort direction (asc/desc, default: asc)
  - `category`: Filter by category
  - `active`: Filter by active status
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "category": "string",
      "price": "number",
      "barcode": "string",
      "active": "boolean",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Get SKU by ID
- **URL**: `/api/skus/{id}`
- **Method**: `GET`
- **Description**: Retrieve a specific SKU by ID
- **Authorization**: Bearer Token
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "category": "string",
  "price": "number",
  "barcode": "string",
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update SKU
- **URL**: `/api/skus/{id}`
- **Method**: `PUT`
- **Description**: Update an existing SKU
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "name": "string",
  "description": "string",
  "category": "string",
  "price": "number",
  "barcode": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "category": "string",
  "price": "number",
  "barcode": "string",
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Delete SKU
- **URL**: `/api/skus/{id}`
- **Method**: `DELETE`
- **Description**: Delete an SKU
- **Authorization**: Bearer Token (Admin only)
- **Response**: `204 No Content`

## Inventory Management

### Get Inventory by Distributor
- **URL**: `/api/inventory/distributor/{distributorId}`
- **Method**: `GET`
- **Description**: Retrieve inventory for a specific distributor
- **Authorization**: Bearer Token
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: skuName)
  - `direction`: Sort direction (asc/desc, default: asc)
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "sku": {
        "id": "string",
        "name": "string"
      },
      "quantity": "number",
      "lastUpdated": "string",
      "updatedBy": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Get Inventory by Outlet
- **URL**: `/api/inventory/outlet/{outletId}`
- **Method**: `GET`
- **Description**: Retrieve inventory for a specific outlet
- **Authorization**: Bearer Token
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: skuName)
  - `direction`: Sort direction (asc/desc, default: asc)
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "sku": {
        "id": "string",
        "name": "string"
      },
      "quantity": "number",
      "lastUpdated": "string",
      "updatedBy": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Update Distributor Inventory
- **URL**: `/api/inventory/distributor/{distributorId}/sku/{skuId}`
- **Method**: `PUT`
- **Description**: Update inventory for a distributor and SKU
- **Authorization**: Bearer Token (Admin, Distributor)
- **Request Body**:
```json
{
  "quantity": "number",
  "operation": "string" // "INCREMENT" or "DECREMENT"
}
```
- **Response**:
```json
{
  "id": "string",
  "sku": {
    "id": "string",
    "name": "string"
  },
  "quantity": "number",
  "lastUpdated": "string",
  "updatedBy": "string"
}
```

### Update Outlet Inventory
- **URL**: `/api/inventory/outlet/{outletId}/sku/{skuId}`
- **Method**: `PUT`
- **Description**: Update inventory for an outlet and SKU
- **Authorization**: Bearer Token (Admin, ASM assigned to outlet)
- **Request Body**:
```json
{
  "quantity": "number",
  "operation": "string" // "INCREMENT" or "DECREMENT"
}
```
- **Response**:
```json
{
  "id": "string",
  "sku": {
    "id": "string",
    "name": "string"
  },
  "quantity": "number",
  "lastUpdated": "string",
  "updatedBy": "string"
}
```

## User Management

### Create User
- **URL**: `/api/users`
- **Method**: `POST`
- **Description**: Create a new user
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "username": "string",
  "password": "string",
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string",
  "phone": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string",
  "phone": "string",
  "active": "boolean",
  "createdAt": "string"
}
```

### Get All Users
- **URL**: `/api/users`
- **Method**: `GET`
- **Description**: Retrieve all users
- **Authorization**: Bearer Token (Admin only)
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: username)
  - `direction`: Sort direction (asc/desc, default: asc)
  - `role`: Filter by role
  - `active`: Filter by active status
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "username": "string",
      "email": "string",
      "firstName": "string",
      "lastName": "string",
      "role": "string",
      "phone": "string",
      "active": "boolean",
      "createdAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Get User by ID
- **URL**: `/api/users/{id}`
- **Method**: `GET`
- **Description**: Retrieve a specific user by ID
- **Authorization**: Bearer Token (Admin or self)
- **Response**:
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string",
  "phone": "string",
  "active": "boolean",
  "createdAt": "string"
}
```

### Update User
- **URL**: `/api/users/{id}`
- **Method**: `PUT`
- **Description**: Update an existing user
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string",
  "phone": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "firstName": "string",
  "lastName": "string",
  "role": "string",
  "phone": "string",
  "active": "boolean",
  "createdAt": "string"
}
```

### Delete User
- **URL**: `/api/users/{id}`
- **Method**: `DELETE`
- **Description**: Delete (deactivate) a user
- **Authorization**: Bearer Token (Admin only)
- **Response**: `204 No Content`

## Outlet Management

### Create Outlet
- **URL**: `/api/outlets`
- **Method**: `POST`
- **Description**: Create a new outlet
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "latitude": "number",
  "longitude": "number",
  "distributorId": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "latitude": "number",
  "longitude": "number",
  "distributor": {
    "id": "string",
    "name": "string"
  },
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Get All Outlets
- **URL**: `/api/outlets`
- **Method**: `GET`
- **Description**: Retrieve all outlets
- **Authorization**: Bearer Token
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: name)
  - `direction`: Sort direction (asc/desc, default: asc)
  - `city`: Filter by city
  - `state`: Filter by state
  - `distributorId`: Filter by distributor
  - `active`: Filter by active status
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "name": "string",
      "address": "string",
      "city": "string",
      "state": "string",
      "pincode": "string",
      "phone": "string",
      "latitude": "number",
      "longitude": "number",
      "distributor": {
        "id": "string",
        "name": "string"
      },
      "active": "boolean",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Get Outlet by ID
- **URL**: `/api/outlets/{id}`
- **Method**: `GET`
- **Description**: Retrieve a specific outlet by ID
- **Authorization**: Bearer Token
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "latitude": "number",
  "longitude": "number",
  "distributor": {
    "id": "string",
    "name": "string"
  },
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update Outlet
- **URL**: `/api/outlets/{id}`
- **Method**: `PUT`
- **Description**: Update an existing outlet
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "latitude": "number",
  "longitude": "number",
  "distributorId": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "latitude": "number",
  "longitude": "number",
  "distributor": {
    "id": "string",
    "name": "string"
  },
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Delete Outlet
- **URL**: `/api/outlets/{id}`
- **Method**: `DELETE`
- **Description**: Delete an outlet
- **Authorization**: Bearer Token (Admin only)
- **Response**: `204 No Content`

### Get Outlets by ASM
- **URL**: `/api/outlets/asm/{asmId}`
- **Method**: `GET`
- **Description**: Retrieve outlets assigned to a specific ASM
- **Authorization**: Bearer Token (Admin, RSM, or the ASM)
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: name)
  - `direction`: Sort direction (asc/desc, default: asc)
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "name": "string",
      "address": "string",
      "city": "string",
      "state": "string",
      "pincode": "string",
      "phone": "string",
      "latitude": "number",
      "longitude": "number",
      "distributor": {
        "id": "string",
        "name": "string"
      },
      "active": "boolean",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Assign ASM to Outlet
- **URL**: `/api/outlets/{outletId}/assign-asm/{asmId}`
- **Method**: `POST`
- **Description**: Assign an ASM to an outlet
- **Authorization**: Bearer Token (Admin only)
- **Response**:
```json
{
  "outletId": "string",
  "asmId": "string",
  "assigned": "boolean"
}
```

### Remove ASM from Outlet
- **URL**: `/api/outlets/{outletId}/remove-asm/{asmId}`
- **Method**: `DELETE`
- **Description**: Remove an ASM from an outlet
- **Authorization**: Bearer Token (Admin only)
- **Response**: `204 No Content`

## Distributor Management

### Create Distributor
- **URL**: `/api/distributors`
- **Method**: `POST`
- **Description**: Create a new distributor
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "email": "string",
  "contactPerson": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "email": "string",
  "contactPerson": "string",
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Get All Distributors
- **URL**: `/api/distributors`
- **Method**: `GET`
- **Description**: Retrieve all distributors
- **Authorization**: Bearer Token
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: name)
  - `direction`: Sort direction (asc/desc, default: asc)
  - `city`: Filter by city
  - `state`: Filter by state
  - `active`: Filter by active status
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "name": "string",
      "address": "string",
      "city": "string",
      "state": "string",
      "pincode": "string",
      "phone": "string",
      "email": "string",
      "contactPerson": "string",
      "active": "boolean",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Get Distributor by ID
- **URL**: `/api/distributors/{id}`
- **Method**: `GET`
- **Description**: Retrieve a specific distributor by ID
- **Authorization**: Bearer Token
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "email": "string",
  "contactPerson": "string",
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Update Distributor
- **URL**: `/api/distributors/{id}`
- **Method**: `PUT`
- **Description**: Update an existing distributor
- **Authorization**: Bearer Token (Admin only)
- **Request Body**:
```json
{
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "email": "string",
  "contactPerson": "string",
  "active": "boolean"
}
```
- **Response**:
```json
{
  "id": "string",
  "name": "string",
  "address": "string",
  "city": "string",
  "state": "string",
  "pincode": "string",
  "phone": "string",
  "email": "string",
  "contactPerson": "string",
  "active": "boolean",
  "createdAt": "string",
  "updatedAt": "string"
}
```

### Delete Distributor
- **URL**: `/api/distributors/{id}`
- **Method**: `DELETE`
- **Description**: Delete a distributor
- **Authorization**: Bearer Token (Admin only)
- **Response**: `204 No Content`

### Get Distributors by RSM
- **URL**: `/api/distributors/rsm/{rsmId}`
- **Method**: `GET`
- **Description**: Retrieve distributors assigned to a specific RSM
- **Authorization**: Bearer Token (Admin or the RSM)
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: name)
  - `direction`: Sort direction (asc/desc, default: asc)
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "name": "string",
      "address": "string",
      "city": "string",
      "state": "string",
      "pincode": "string",
      "phone": "string",
      "email": "string",
      "contactPerson": "string",
      "active": "boolean",
      "createdAt": "string",
      "updatedAt": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Assign RSM to Distributor
- **URL**: `/api/distributors/{distributorId}/assign-rsm/{rsmId}`
- **Method**: `POST`
- **Description**: Assign an RSM to a distributor
- **Authorization**: Bearer Token (Admin only)
- **Response**:
```json
{
  "distributorId": "string",
  "rsmId": "string",
  "assigned": "boolean"
}
```

### Remove RSM from Distributor
- **URL**: `/api/distributors/{distributorId}/remove-rsm/{rsmId}`
- **Method**: `DELETE`
- **Description**: Remove an RSM from a distributor
- **Authorization**: Bearer Token (Admin only)
- **Response**: `204 No Content`

## Attendance Management

### Mark Attendance
- **URL**: `/api/attendance`
- **Method**: `POST`
- **Description**: Mark attendance at an outlet
- **Authorization**: Bearer Token (ASM only)
- **Request Body**:
```json
{
  "outletId": "string",
  "latitude": "number",
  "longitude": "number",
  "notes": "string"
}
```
- **Response**:
```json
{
  "id": "string",
  "outlet": {
    "id": "string",
    "name": "string"
  },
  "user": {
    "id": "string",
    "username": "string"
  },
  "checkInTime": "string",
  "latitude": "number",
  "longitude": "number",
  "validLocation": "boolean",
  "notes": "string"
}
```

### Get Attendance History for ASM
- **URL**: `/api/attendance/asm/{asmId}`
- **Method**: `GET`
- **Description**: Retrieve attendance history for a specific ASM
- **Authorization**: Bearer Token (Admin, RSM, or the ASM)
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: checkInTime)
  - `direction`: Sort direction (asc/desc, default: desc)
  - `startDate`: Filter by start date (format: YYYY-MM-DD)
  - `endDate`: Filter by end date (format: YYYY-MM-DD)
  - `outletId`: Filter by outlet
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "outlet": {
        "id": "string",
        "name": "string"
      },
      "user": {
        "id": "string",
        "username": "string"
      },
      "checkInTime": "string",
      "latitude": "number",
      "longitude": "number",
      "validLocation": "boolean",
      "notes": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

### Get Attendance History for Outlet
- **URL**: `/api/attendance/outlet/{outletId}`
- **Method**: `GET`
- **Description**: Retrieve attendance history for a specific outlet
- **Authorization**: Bearer Token (Admin, RSM)
- **Query Parameters**:
  - `page`: Page number (default: 0)
  - `size`: Page size (default: 20)
  - `sort`: Sort field (default: checkInTime)
  - `direction`: Sort direction (asc/desc, default: desc)
  - `startDate`: Filter by start date (format: YYYY-MM-DD)
  - `endDate`: Filter by end date (format: YYYY-MM-DD)
  - `asmId`: Filter by ASM
- **Response**:
```json
{
  "content": [
    {
      "id": "string",
      "outlet": {
        "id": "string",
        "name": "string"
      },
      "user": {
        "id": "string",
        "username": "string"
      },
      "checkInTime": "string",
      "latitude": "number",
      "longitude": "number",
      "validLocation": "boolean",
      "notes": "string"
    }
  ],
  "totalElements": "number",
  "totalPages": "number",
  "size": "number",
  "number": "number"
}
```

## Reports

### Generate Inventory Report
- **URL**: `/api/reports/inventory`
- **Method**: `GET`
- **Description**: Generate inventory report
- **Authorization**: Bearer Token (Admin, Management, RSM)
- **Query Parameters**:
  - `format`: Report format (PDF/EXCEL, default: EXCEL)
  - `skuId`: Filter by SKU
  - `distributorId`: Filter by distributor
  - `outletId`: Filter by outlet
  - `state`: Filter by state
  - `city`: Filter by city
  - `asOfDate`: As of date (format: YYYY-MM-DD, default: current date)
- **Response**: Binary file (PDF or Excel)

### Generate Attendance Report
- **URL**: `/api/reports/attendance`
- **Method**: `GET`
- **Description**: Generate attendance report
- **Authorization**: Bearer Token (Admin, Management, RSM)
- **Query Parameters**:
  - `format`: Report format (PDF/EXCEL, default: EXCEL)
  - `asmId`: Filter by ASM
  - `outletId`: Filter by outlet
  - `distributorId`: Filter by distributor
  - `state`: Filter by state
  - `city`: Filter by city
  - `startDate`: Start date (format: YYYY-MM-DD, required)
  - `endDate`: End date (format: YYYY-MM-DD, required)
- **Response**: Binary file (PDF or Excel)

### Generate Daily Inventory Report
- **URL**: `/api/reports/inventory/daily`
- **Method**: `GET`
- **Description**: Generate daily inventory report
- **Authorization**: Bearer Token (Admin, Management, RSM)
- **Query Parameters**:
  - `format`: Report format (PDF/EXCEL, default: EXCEL)
  - `distributorId`: Filter by distributor
  - `state`: Filter by state
  - `city`: Filter by city
  - `date`: Report date (format: YYYY-MM-DD, default: current date)
- **Response**: Binary file (PDF or Excel) 