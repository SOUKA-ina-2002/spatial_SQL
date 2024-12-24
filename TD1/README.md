# TD1: Getting Started with Spatial SQL

This guide provides a detailed walkthrough for installing PostGIS and setting up your first spatial database. PostGIS is a powerful spatial database extender for PostgreSQL, enabling advanced GIS operations within a relational database system.

## Prerequisites

- PostgreSQL installed on your system.
- Internet access to download necessary extensions and tools.

## Steps to Follow

### 1. Install PostgreSQL
1. Visit the [PostgreSQL Downloads Page](https://www.postgresql.org/download/) and download the appropriate version for your operating system (Windows, macOS, or Linux).
2. Follow the installation guide and set up PostgreSQL on your system.
3. During the installation, set a password for the `postgres` user.

### 2. Install PostGIS
1. During the PostgreSQL installation, ensure you select all components, including the **Stack Builder** tool.
2. Launch the Stack Builder and select the PostgreSQL version you installed.
3. In the application selection list, choose **PostGIS**.
4. Complete the installation following the prompts.

### 3. Create Your First Spatial Database
1. Open **pgAdmin 4**, the PostgreSQL database management tool.
2. Connect to the PostgreSQL server using the credentials set during installation.
3. Right-click on `Databases` and select `Create > Database`.
4. Provide a name for your database (e.g., `spatial_db`) and save it.
5. Open the `Query Tool` for your database and run the following command to enable PostGIS:

   ```sql
   CREATE EXTENSION postgis;
   ```
6. Verify the installation by checking for the `spatial_ref_sys` table under `Schemas > Public > Tables`.

## Next Steps

Once your spatial database is set up, you can move on to creating tables with spatial columns and performing GIS operations using SQL. Check out **TD2** for more information on creating spatial tables.

## Resources
- [PostGIS Documentation](https://postgis.net/documentation/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

Feel free to reach out if you encounter any issues or need further assistance!
