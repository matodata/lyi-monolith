---
layout: default
---

# LYI Monolith Documentation

Welcome to the LYI Monolith documentation. This site provides comprehensive documentation for the API endpoints and database models used in the application.

## Documentation

- [API Documentation](apis.html): Complete documentation of all API endpoints, including request/response formats, authentication requirements, and descriptions.
- [Database Models](models.html): Detailed documentation of all database entities, their relationships, and field descriptions.

## Project Overview

The LYI Monolith application is designed to support:

1. **Inventory Management**
   - Track inventory of SKUs across distributors and outlets
   - Generate inventory reports
   - Manage SKUs (Create, Read, Update, Delete)
   - Increment and decrement stock for SKUs

2. **Employee Tracking**
   - Track ASM attendance at outlets
   - Verify outlet visits using geo-fencing
   - Generate attendance reports

### User Roles

- **Admin**: Full system access with user management capabilities
- **Management**: Report generation and system monitoring
- **Regional Sales Manager (RSM)**: Manage distributors and related outlets
- **Area Sales Manager (ASM)**: Manage outlets and inventory on behalf of assigned outlets
- **Distributor**: Manage inventory for their own operations

## Getting Started

For developers, refer to the main [README.md](https://github.com/matodata/lyi-monolith) file in the repository for setup instructions. 