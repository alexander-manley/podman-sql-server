# Containerized MS SQL Server + Machine Learning Services
# T-SQL + Python/R ML
https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-machine-learning-docker?view=sql-server-ver16

# Base Image
podman pull mcr.microsoft.com/mssql/server:2022-latest

# Rebuild with ML Services (Update Dockerfile: FROM ubuntu:22:04) (9.15GB)
git clone https://github.com/microsoft/mssql-docker mssql-docker
cd mssql-docker/linux/preview/examples/mssql-mlservices
podman build -t mssql-server-2022-mlservices .

# Launch Developer + ML Services
podman run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=password -e "MSSQL_PID=Developer" -v /mnt/c/Users/Alexander/Desktop/Data/mssql-server-data:/var/opt/mssql -p 1433:1433 mssql-server-2022-mlservices

# Launch Express + ML Services
podman run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=password -e "MSSQL_PID=Express" -v /mnt/c/Users/Alexander/Desktop/Data/mssql-server-data:/var/opt/mssql -p 1433:1433 mssql-server-2022-mlservices

# Manage with SQL Server Management Studio & Azure Data Studio
https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms-19?view=sql-server-ver16

# SSMS download:
https://go.microsoft.com/fwlink/?linkid=2195969&clcid=0x409
