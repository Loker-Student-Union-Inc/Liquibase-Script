# Liquibase-Script

## Overview

This repository contains the Liquibase configuration and changelogs for managing database schema changes within the CSUDH LSU persistence project. The Liquibase scripts enable seamless database schema management, ensuring consistency and traceability across various environments including development, testing, and production.

## Why Liquibase?

Liquibase is a robust, industry-standard database migration tool that offers a comprehensive solution for version-controlling and managing schema changes. It provides an automated and reliable way to evolve your database schema alongside your application code.

### Key Benefits

- **Cross-Environment Consistency**: Liquibase ensures that schema changes are consistently applied across all environments, from local development to production, reducing the risk of discrepancies.
- **Automated Deployments**: Integrate Liquibase into your CI/CD pipeline to automate schema updates during deployments, minimizing manual intervention and the potential for errors.
- **Change History and Auditing**: Liquibase maintains a detailed history of all schema changes, enabling easy auditing and rollback capabilities, essential for compliance and debugging.
- **Safe Rollback**: In the event of an issue, Liquibase's rollback functionality allows you to safely revert to a previous state, preserving data integrity.
- **TTL Management**: With CockroachDB's Time to Live (TTL) feature, Liquibase allows automatic purging of stale data, crucial for managing large datasets and optimizing storage.

## Getting Started

### Prerequisites

Ensure you have the following installed:

- [Java 17](https://www.oracle.com/java/technologies/javase-jdk17-downloads.html)
- [Gradle 7.5](https://gradle.org/install/)
- [CockroachDB](https://www.cockroachlabs.com/docs/stable/install-cockroachdb.html)

### Repository Setup

To set up the project locally, follow these steps:

1. **Clone the Repository**

   Begin by cloning the repository to your local environment:

   ```bash
   git clone https://github.com/Loker-Student-Union-Inc/Liquibase-Script.git
   cd Liquibase-Script
   ```

2. **Configure the Database**

   Ensure that your CockroachDB instance is running and accessible. Update the `application.properties` file with the appropriate database credentials.

3. **Apply Schema Changes**

   Liquibase scripts are executed automatically during the application startup. However, you can manually apply them by running:

   ```bash
   ./gradlew update
   ```

   This command applies all pending changelogs to the target database, ensuring that the schema is up-to-date.

### Verifying TTL Configuration

After running the Liquibase scripts, you can verify that the TTL settings are correctly applied to your tables using the following SQL query:

```sql
SELECT loc, published_event, create_timestamp, crdb_internal_expiration
FROM LOC_EVENT;
```

This query helps confirm that the TTL is functioning as expected, with the `crdb_internal_expiration` column reflecting the correct expiration times.

### Additional Information

- **Changelog Directory**: All Liquibase changelogs are stored under `src/main/resources/db/changelog/`. The `master.xml` serves as the entry point for all changesets.
- **Migration Directory**: For raw SQL migrations, refer to `src/main/resources/db/migration/`.

### Contributing

We welcome contributions from the community. Please follow the standard Git workflow for submitting changes:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/new-feature`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to the branch (`git push origin feature/new-feature`).
5. Create a pull request.

### Contact

For any queries or support, please contact the repository maintainers.