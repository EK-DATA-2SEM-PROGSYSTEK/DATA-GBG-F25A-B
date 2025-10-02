# Opgave: emp_dept med JdbcTemplate

I denne opgave skal vi bruge databasen emp_dept_25 sammen med java-projektet.

1. Klon projektet  [EmpJDBC](https://github.com/SigneBorch/EmpJDBC.git) fra GitHub.
2. Sæt environment-variable i IntelliJ så de passer til dine database credentials. Kopier variabelnavnene fra application_properties filen i projektet. Værdierne på højre side af lighedstegnet skal ligne dem vi brugte i jdbctemplate_standalone når vi lavede vores DataSource, men skift databasenavnet så det er den vi skal bruge her, nemlig emp_dept_25 (i stedet for jdbctemplate_test).
4. Klik på pilen til højre for klassen der kører (øverst til højre i menulinjen) for at åbne "Edit configurations". I dette projekt hedder klassen EmpJDBCApplication.
   
   <img src="Billede1.png" alt="Alt Text" width="200">
   
6. Der kommer et vindue op hvor man kan konfigurere. Klik på "modify options" og vælg "Environment variables" - så kommer feltet frem I kan skrive i.

   <img src="Billede2.png" alt="Alt Text" width="600">
   
   Formen på det i skriver i boksen er: DEV_DATABASE_URL=jdbc:mysql://localhost:3306/emp_dept_25.

   <img src="Billede3.png" alt="Alt Text" width="500">
   
   Skriv de tre variable DEV_DATABASE_URL, DEV_USERNAME og DEV_PASSWORD, og assign dem værdier (root til brugernavnet, og jeres personlige databasepassword til passwordet).

   De tre variable svarer til de variable I har stående inde i application_properties filen i projektet.

   <img src="Billede4.png" alt="Alt Text" width="500">
   
8. Når I har skrevet de tre variable, separeret med semikolon, så tryk apply.
  
9. Kør programmet.

    Det er nu disse variable der bruges inde i Repository-klassen.
   
   <img src="Billede5.png" alt="Alt Text" width="500">
