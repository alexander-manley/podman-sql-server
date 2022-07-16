# Containerized MS SQL Server + Machine Learning Services
# T-SQL + Python/R ML
https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-machine-learning-docker?view=sql-server-ver16
https://hub.docker.com/_/microsoft-mssql-server

# Base Image
podman pull mcr.microsoft.com/mssql/server:2022-latest

# Rebuild with ML Services (Update Dockerfile: FROM ubuntu:22:04) (9.15GB)
git clone https://github.com/microsoft/mssql-docker mssql-docker
cd mssql-docker/linux/preview/examples/mssql-mlservices
podman build -t mssql-server-2022-mlservices .

# Launch Developer v2019
podman run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=Passw0rd -e "MSSQL_PID=Developer" -v /mnt/c/Users/Alexander/Desktop/Data/mssql-server-data:/var/opt/mssql/data -p 1433:1433 --name mssql-server-2019 mcr.microsoft.com/mssql/server:2019-latest

# Launch Developer v2022 + ML Services
podman run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=Passw0rd -e "MSSQL_PID=Developer" -v /mnt/c/Users/Alexander/Desktop/Data/mssql-server-data:/var/opt/mssql/data -p 1433:1433 --name mssql-server-2022-mlservices mssql-server-2022-mlservices

# Launch Express v2022 + ML Services
podman run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=Passw0rd -e "MSSQL_PID=Developer" -v /mnt/c/Users/Alexander/Desktop/Data/mssql-server-data:/var/opt/mssql/data -p 1433:1433 --name mssql-server-2022-mlservices mssql-server-2022-mlservices

# Terminal for v2019 (no sqlcmd for v2022-Beta)
podman exec -it mssql-server-2022-mlservices /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P Passw0rd

# Activate ML Services via T-SQL
### OUTPUT: Configuration option 'external scripts enabled' changed from 0 to 1. Run the RECONFIGURE statement to install.
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE

# Manage with SQL Server Management Studio & Azure Data Studio
https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms-19?view=sql-server-ver16

# SSMS download:
https://go.microsoft.com/fwlink/?linkid=2195969&clcid=0x409
