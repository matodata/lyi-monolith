# LYI Monolith

Spring Boot monolith application for the LYI project.

## Setup Requirements

- Java 17 or higher
- Gradle (or use the included Gradle wrapper)

## Project Structure

This is a standard Spring Boot application with the following structure:

```
src/main/java/com/matodata/lyi/      - Java source files
src/main/resources/                  - Configuration files and static resources
src/test/                            - Test files
docs/                                - Documentation (published as GitHub Pages)
```

## Running the Application

To build and run the application:

```bash
# Using Gradle wrapper
./gradlew bootRun

# Or if you have Gradle installed
gradle bootRun
```

The application will start on port 8080 by default.

## Development

### Building the project

```bash
./gradlew build
```

### Running tests

```bash
./gradlew test
```

### Creating a production build

```bash
./gradlew bootJar
```

The resulting JAR file will be in `build/libs/` directory.

## Documentation

The API and database model documentation is available in the `docs` directory and is published as GitHub Pages.

To view the documentation:
1. Navigate to `https://[your-github-username].github.io/lyi-monolith/`
2. View the API documentation at `/apis.html` 
3. View the database model documentation at `/models.html`

To update the documentation:
1. Edit the files in the `docs` directory
2. Commit and push your changes to trigger the GitHub Pages workflow

## Database

The application is configured to use H2 in-memory database for development purposes.
The H2 console is enabled and can be accessed at `http://localhost:8080/h2-console` when the application is running.

Database connection details (for development):
- JDBC URL: `jdbc:h2:mem:lyidb`
- Username: `sa`
- Password: `password`

## Technologies

- Spring Boot 3.2.3
- Spring Web
- Spring Data JPA
- H2 Database (for development)
- Lombok
- Java 17

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
