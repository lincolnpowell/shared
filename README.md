# Shared Household Agreed Reimbursement Expense Dissemination (SHARED) System
[![GitHub License](https://img.shields.io/github/license/lincolnpowell/shared?style=flat-square&label=License&logo=GitHub)](LICENSE)
[![GitHub Release](https://img.shields.io/github/v/release/lincolnpowell/shared?style=flat-square&logo=GitHub&label=Release)](https://github.com/lincolnpowell/shared/releases)
<a href="#">![GitHub repo size](https://img.shields.io/github/repo-size/lincolnpowell/shared?style=flat-square&logo=GitHub&label=Repo%20Size)</a>
[![Docker](https://img.shields.io/badge/Docker-1D63ED?style=flat-square&logo=Docker&logoColor=FFFFFF)](https://www.docker.com/products/docker-desktop/)
[![Blazor](https://img.shields.io/badge/Blazor-582B8E?style=flat-square&logo=Blazor&logoColor=FFFFFF)](https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor)

## Problem Statement
Each month, all shared household-related invoices and/or receipts need to be manually itemized for equitable reimbursement to owed parties. This process is very error-prone and time-consuming.

## Intent
The intent of this project is to create a semi-automated solution, dubbed "Shared Household Agreed Reimbursement Expense Dissemination" or SHARED, with the following features:

- Intelligently select an item's equitable reimbursement percentage based on prior data
- Allow override of equitable reimbursement before invoice or receipt submission
- Generate monthly report detailing how much money should be reimbursed for shared household expenses (e.g. household-related bills, shared grocery items, etc.) based on individual
- Email delivery to all individuals

## Dependencies
- [Git for Windows](https://gitforwindows.org/): _Optional if you already have Git installed or are using a non-Windows OS_
- [Docker](https://docs.docker.com/get-docker/)
- [Visual Studio Community 2022](https://visualstudio.microsoft.com/)
- [Microsoft SQL Server Management Studio](https://learn.microsoft.com/en-us/ssms/download-sql-server-management-studio-ssms)
- [LINQPad](https://www.linqpad.net/): _Optional_

## Build
1. Clone the project to a local destination of your choice via:
    ```
    git clone https://github.com/lincolnpowell/shared.git
    ```
    > **DO NOT** open Visual Studio at this time! You will need to complete the next step beforehand; else, Docker will fail to create the MSSQL Server database container upon opening the project.
1. Create an `.env` file within the "Shared" directory of this project with the following contents:
    ```
    ACCEPT_EULA=Y
    MSSQL_SA_PASSWORD=''
    ```
1. Using Visual Studio, open the Shared.sln solution file to view the SHARED project.
    > At this time, Visual Studio will automatically create the Docker containers for the project. This may take a few minutes to complete.
1. Using Docker Desktop, verify that the `db` container is running within the `shared` compose stack.
    > You may need to change the exposed port number if you are running another MSSQL Server instance using 1433.

## Setup
### Microsoft SQL Server Management Studio
1. Open Microsoft SQL Server Management Studio and connect to the `db` container using the following:
    ```
    Server type: Database Engine
    Server name: localhost
    Authentication: SQL Server Authentication
    Login: sa
    Password: <MSSQL_SA_PASSWORD value you provided in the .env file above>
    Enable "Trust server certificate"
    ```
1. Click "Connect" to establish the connection.

### LINQPad
1. Open LINQPad and click "Add connection" in the top left corner. Select "LINQ to SQL (optimized for SQL Server)" and enter the following:
    ```
    Provider: SQL Server
    Server: localhost
    Select "SQL Authentication"
    User name: sa
    Password: <MSSQL_SA_PASSWORD value you provided in the .env file above>
    ```
1. Click "Test" button to verify the connection. If successful, click "OK" to save the connection. You can now use LINQPad to query the database.

## Run
Ensure "docker-compose" is set as the startup item in Visual Studio. Click the "Run" button to start the application.

The web application will be available at `https://localhost:60166/` in your web browser.

SwaggerUI can be accessed at `https://localhost:60165/swagger/index.html` to view the API endpoints.