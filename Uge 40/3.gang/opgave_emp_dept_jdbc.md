# Opgave: emp_dept med JdbcTemplate

1. Klon projektet  [EmpJDBC](https://github.com/SigneBorch/EmpJDBC.git) fra GitHub.
2. Sæt environment-variable i IntelliJ så de passer til dine database credentials. Kopier variabelnavnene fra application_properties filen i projektet. Værdierne på højre side af lighedstegnet skal ligne dem vi brugte i jdbctemplate_standalone når vi lavede vores DataSource, men skift databasenavnet så det er den vi skal bruge her, nemlig emp_dept_25 (i stedet for jdbctemplate_test).
3. Klik på pilen til højre for klassen der kører (øverst til højre i menulinjen) for at åbne "Edit configurations". I dette projekt hedder klassen EmpJDBCApplication.
4. Der kommer et vindue op hvor man kan konfigurere. Klik på "modify options" og vælg "Environment variables" - så kommer feltet frem I kan skrive I. Når I har skrevet de tre variable, separeret med semikolon, så tryk apply.
  
5. Kør programmet.
