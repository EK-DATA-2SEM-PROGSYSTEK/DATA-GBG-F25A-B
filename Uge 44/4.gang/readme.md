# Fejlhåndtering i Spring Boot

## Vi implementerer best practices for fejlhåndtering i vores Spring Boot applikation

## Forberedelse
Kig på koden for en simpel CRUD applikation med fejlhåndtering i Spring Boot her: [fejlhåndtering demo](https://github.com/EK-DATA-2SEM-PROGSYSTEK/profile-error-handling.git) og 
noterer hvordan fejlhåndtering er implementeret.
(Der forventes ikke at man forstår det hele. Der vil være annoteringer som er ukendte - dem kigger vi på sammen)

---

## Læringsmål

- at kunne implementere fejlhåndtering i en Spring Boot applikation
- at kunne anvende best practices for fejlhåndtering i en Spring Boot applikation
- at kunne anvende globale og lokale fejlhåndteringsmekanismer i Spring Boot

---

## Indhold

- custom error pages
- custom exceptions
- @ControllerAdvice, @ExceptionHandler, @ResponseStatus

---

### Fejlhåndtering i Spring Boot

---

### Custom Error Pages

Spring Boot har en indbygget fejlmekanisme som automatisk håndterer alle fejl og exceptions i web-laget.


Når en fejl opstår (f.eks. 404 eller 500), forsøger Spring Boot at finde en passende HTML-skabelon 
og vise den i stedet for den indbyggede Whitelabel Error Page.


Spring Boot leder automatisk efter filer i følgende rækkefølge:
1.	/templates/error/<status>.html (fx error/404.html)
2.	/templates/error.html (generisk fallback)
3.	Hvis ingen findes → vises den indbyggede Whitelabel Error Page (medmindre slået fra).


For at oprette brugerdefinerede fejlsider, skal HTML-filerne i følgende mapper:
```text
src/
└── main/
    └── resources/
        └── templates/
            └── error/
            ├── 404.html
            ├── 500.html
            └── error.html
```

---


### Custom Exceptions

Ved at implementere custom exceptions (som nedarver fra fx RuntimeException) 
kan man skabe mere meningsfulde fejlmeddelelser og håndtere specifikke fejlscenarier i en applikation.

Desuden opnåes der lag-separation dvs. at service/repo kender domænefejl; web-laget beslutter HTTP-respons og visning.

Her ses et eksempel på en custom exception hvor en profil allerede eksisterer.

```@ResponseStatus``` annotationen sætte HTTP-statuskoden, som Spring skal returnere, når en exception opstår.

```java
@ResponseStatus(HttpStatus.CONFLICT)
public class DuplicateProfileException extends RuntimeException {
    public DuplicateProfileException(String message) {
        super(message);
    }
}


```
Når der forsøges at oprette en profil med et navn eller email der allerede eksisterer, 
vil UNIQUE constraint i databasen få JdbcTemplate metoden til at kaste en DataIntegrityViolationException.
Denne exception kan fanges i service-laget og omsættes til en DuplicateProfileException som giver mere mening i domænet.


```java
    public Profile create(Profile profile) {
        try {
            return repo.insert(profile);
        } catch (DataIntegrityViolationException e) {
            throw new DuplicateProfileException(
                    "A profile with this name or email already exists."
            );
        } catch (DataAccessException dataAccessException) {
            throw new DatabaseOperationException("Failed to create profile", dataAccessException);
        }
    }
```

---


### Global Fejlhåndtering med ```@ControllerAdvice```

```@ControllerAdvice``` er en Spring-annotation, der bruges til at gruppere globale fejlhåndteringsmekanismer ét centralt sted.

Det gør det lettere at håndtere exceptions på tværs af forskellige controllere samt at vedligeholde fejlhåndteringslogik.

Dette gøres typisk ved at bruge ```@ExceptionHandler``` annotationen på metoder inde i en klasse, der er markeret med ```@ControllerAdvice```.

Sagt på en anden måde: “Hvis denne type fejl/exception sker, så bruge denne metode til at håndtere den.”


```java

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ProfileNotFoundException.class)
    public String handleNotFound(ProfileNotFoundException ex, Model model) {
        model.addAttribute("status", HttpStatus.NOT_FOUND.value());
        model.addAttribute("error", "Not Found");
        model.addAttribute("message", ex.getMessage());
        return "error/404";
    }

    @ExceptionHandler(DuplicateProfileException.class)
    public String handleDuplicate(DuplicateProfileException ex, Model model) {
        model.addAttribute("status", HttpStatus.CONFLICT.value());
        model.addAttribute("error", "Duplicate Entry");
        model.addAttribute("message", ex.getMessage());
        return "error/error";
    }
```

---


## Aktiviteter

[Opgave: Fejlhåndtering i Spring Boot](opgave-fejlhaandtering.md)

Fejlhåndtering i projektet

Delphi undersøgelse
