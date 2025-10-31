### Opgave: Fejlhåndtering i Sprint Boot

Formålet med opgaven er at kunne forklare og implementere fejlhåndtering 
i en Spring Boot applikation ved hjælp af best practices.

Opgaven skal laves parvis.


1. Fork repoen fra [profile_error_handling](https://github.com/EK-DATA-2SEM-PROGSYSTEK/profile-error-handling.git)

2. I MySQLWorkbench (eller DataGrip), kør `schema.sql` og efterfølgende `data.sql` scripterne 
som findes i projektets resources mappe for at oprette en lokale database og indsætte testdata.

3. I IntelliJ tilføj environment variablerne for databaseforbindelsen i `Run/Debug Configurations`:
   - `DEV_DB_URL=jdbc:mysql://localhost:3306/exceptional_profiles`
   - `DEV_DB_USERNAME=<YOUR_USERNAME_HERE>`
   - `DEV_DB_PASSWORD=<YOUR_PASSWORD_HERE>`

4. Kør applikationen og test at den virker ved at åbne `http://localhost:8080/profiles` i din browser.

---

#### Fejlhåndtering

5. Ændr urlen i browseren til `http://localhost:8080/profile` og observer resultatet. Forklar til hinanden hvordan fejlen
håndteres i koden.

6. Ændr urlen tilbage til `http://localhost:8080/profiles` og opret en ny profil ved at klikke på `Create New Profile` knappen.
Indtast navnet "Freja Hansen" en email adresse og klik `Save`. Observer resultatet og forklar til hinanden hvordan fejlen
håndteres i koden.

7. Ændr urlen i browseren til http://localhost:8080/profiles/9/edit . Observer resultatet og forklar til hinanden hvordan fejlen
   håndteres i koden.


