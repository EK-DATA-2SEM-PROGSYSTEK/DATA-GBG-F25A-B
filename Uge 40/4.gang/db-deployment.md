### MySQL Deployment på Azure

Denne guide beskriver, hvordan man opretter en MySQL database server på Azure 
og efterfølgende opretter en MySQL database ved brug af f.eks. MySQL Workbench.

Det kræver at man har oprettet en konto på Azure og er logget ind i [Azure portalen](https://portal.azure.com)

1. Under Azure services vælg Azure Database for MySQL servers. Hvis Azure Database for MySQL servers er synlig, 
søg efter den i søgefeltet øverst på siden.

<img src="assets/azure-db-for-mysql.png" alt="Azure DB for MySQL" width="900">

2. Klik på + Create for at oprette en ny MySQL server.

<img src="assets/create-mysql-server.png" alt="Create MySQL Server" width="900">

3. Vælg ”Flexible server” og ”Quick Create”

<img src="assets/flexible-server.png" alt="Flexible Server" width="900">

4. Konfigurer serveren:
    1. Opret en ressource group med et passende navn
   2. Skriv et servernavn
   3. Vælg Region ”North Europe”
   4. Angiv et login og password (husk det)
   5. Vælg ”’Dev/Test” som Workload type
   6. Vælg ”Add firewall rule for current IP address”
   7. Vælg “Review + create”

<img src="assets/configure-server.png" alt="Configure MySQL Server" width="900">

5. Vælg ”Create” for at oprette serveren.

<img src="assets/create-server.png" alt="Create MySQL Server" width="900">

6. En “Deployment is in progress” side vises mens serveren oprettes (det tager flere minutter).

<img src="assets/deployment-in-progress.png" alt="Deployment in progress" width="900">

7. Når deployment er færdigt, vælg ”Go to resource”.

<img src="assets/deployment-complete.png" alt="Deployment complete" width="900">

8. Noter ”Server name” url: 

<img src="assets/server-resource.png" alt="Server resource" width="900">

9. Vælg ”Settings” og herunder vælg ”Networking” 
    1. Vælg ”Allow public access from any Azure service within Azure to this server”
    2. Vælg "+ Add current client IP address" (Dette skal gentages hvis klient IP adressen ændres)
   3. Vælg ”Save”

NB. Dette er meget vigtigt, ellers kan den deployede applikation ikke få adgang til databasen.

<img src="assets/allow-access.png" alt="Allow access" width="900">


10. En MySQL server er nu oprettet på Azure og der kan nu oprettes en database ved brug af f.eks. MySQL Workbench.
    1.	Opret en ny forbindelse

<img src="assets/workbench-new-connection.png" alt="MySQL Workbench New Connection" width="900">


11. Opsæt den nye forbindelse med:
    1. et navn
    2. hostname som er urlen af den server oprettet tidligere på Azure
    3. Username og Password som blev angivet ved optrettelsen af serveren
    4. Vælg ”Test Connection”

<img src="assets/configure-connection.png" alt="MySQL Workbench Connection Setup" width="900">

12. Et ”Successfully made the MySQL connection” vindue vises.

<img src="assets/test-connection.png" alt="MySQL Workbench Successful Connection" width="900">

13. Vælg forbindelsen og opret en database ved MySQL Workbench som normalt.

