# Databasetransaktioner


## Beskrivelse
I dag skal vi se på databasetransaktioner og hvordan vi arbejder med dem.  
En transaktion er en unit of work, hvor vi skal sikre at enten alt eller intet går godt. Vi kan ikke efterlade databasen i inkonsistent tilstand. Tænk f.eks. overførsel via mobilepay, hvor beløb trækkes fra din egen konto, men aldrig overføres til modtagers konto.

Nøgleordene i løsning hedder “commit” og “rollback”.


## Forberedelse
Se denne video:  
[What is a Database Transaction? Be ACID compliant!](https://www.youtube.com/watch?v=wHUOeXbZCYA)  
[JDBC Transactions in Java 💳 | Commit, Rollback & Auto-Commit Explained](https://www.youtube.com/watch?v=waWcHof2S-g)

Læs om transaktioner på [Baeldung](http://www.baeldung.com/sql/mysql-transaction-management-statements).  
Læs [denne beskrivelse](http://en.wikipedia.org/wiki/Database_transaction) på wiki om database transaktioner (kun til og med afsnittet “Transactional databases”.


## Læringsmål
- At forstå og anvende transaktioner i databasen.

## Indhold

## Databasetransaktioner i Spring Boot (JDBC Template)

### Hvad er en transaktion?
En **transaktion** er en sekvens af én eller flere databaseoperationer, som enten **alle skal gennemføres**, eller **ingen skal**.  
Transaktioner sikrer **dataintegritet**, selvom der opstår fejl undervejs.

De fire grundlæggende egenskaber ved en transaktion kaldes **ACID**:

| Egenskab | Forklaring |
|-----------|-------------|
| **A – Atomicity** | Alt eller intet: Hvis én del fejler, rulles alt tilbage. |
| **C – Consistency** | Databasen skal gå fra én gyldig tilstand til en anden. |
| **I – Isolation** | Parallelle transaktioner må ikke påvirke hinanden utilsigtet. |
| **D – Durability** | Når en transaktion er committed, bliver ændringerne gemt permanent. |

---

### Eksempel: Overfør penge mellem to konti

I dette eksempel anvender vi `JdbcTemplate` og `DataSourceTransactionManager` til manuelt at styre transaktionen.  
Hvis overførslen til den ene konto fejler, rulles hele transaktionen tilbage.

```java
package com.example.demo.bank;

import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.DefaultTransactionDefinition;

@Repository
public class BankRepository {

    private final JdbcTemplate jdbcTemplate;
    private final DataSourceTransactionManager transactionManager;

    public BankRepository(JdbcTemplate jdbcTemplate, DataSourceTransactionManager transactionManager) {
        this.jdbcTemplate = jdbcTemplate;
        this.transactionManager = transactionManager;
    }

    public void transferMoney(int fromAccountId, int toAccountId, double amount) {
        String withdrawSql = "UPDATE account SET balance = balance - ? WHERE id = ?";
        String depositSql = "UPDATE account SET balance = balance + ? WHERE id = ?";

        // Start en ny transaktion
        TransactionStatus status = transactionManager.getTransaction(new DefaultTransactionDefinition());

        try {
            // Træk beløb fra afsender
            jdbcTemplate.update(withdrawSql, amount, fromAccountId);

            // Indsæt beløb på modtager
            jdbcTemplate.update(depositSql, amount, toAccountId);

            // Commit transaktionen hvis alt lykkes
            transactionManager.commit(status);
            System.out.println("Transaktion gennemført!");

        } catch (Exception e) {
            // Rul tilbage ved fejl
            transactionManager.rollback(status);
            System.err.println("Fejl! Transaktion rullet tilbage.");
            throw new RuntimeException("Fejl under pengeoverførsel", e);
        }
    }
}

```

### Transaktioner med @Transactional annotation

Spring kan automatisk håndtere transaktioner for os via annotationen @Transactional.
Spring åbner og lukker selv en transaktion omkring metoden — og laver automatisk rollback, hvis der opstår en runtime-fejl.

```java
@Service
public class BankService {

    private final JdbcTemplate jdbcTemplate;

    public BankService(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    @Transactional
    public void transferMoney(int fromAccountId, int toAccountId, double amount) {
        String withdrawSql = "UPDATE account SET balance = balance - ? WHERE id = ?";
        String depositSql = "UPDATE account SET balance = balance + ? WHERE id = ?";

        jdbcTemplate.update(withdrawSql, amount, fromAccountId);
        jdbcTemplate.update(depositSql, amount, toAccountId);
    }
}
```
Hvad sker der her?

- @Transactional fortæller Spring, at metoden skal køre som én transaktion.

- Hvis en RuntimeException opstår, laver Spring automatisk rollback.

- Hvis alt lykkes, bliver transaktionen committed.

### Sammanligning  

| Egenskab | Manuel styring med `Connection` | Automatisk styring med `@Transactional` |
|-----------|--------------------------------|-----------------------------------------|
| **Kontrol** | Fuld kontrol over `commit` og `rollback` | Spring håndterer transaktionen automatisk |
| **Fejl-håndtering** | Skal skrives manuelt med `try/catch` og `rollback()` | Automatisk rollback ved `RuntimeException` |
| **Brugervenlighed** | Mere kode og flere detaljer at huske | Enkel, læsbar og mindre fejlbehæftet |
| **Fleksibilitet** | God ved meget komplekse forløb | Velegnet til de fleste scenarier |
| **Ydelse** | Ingen ekstra overhead | En smule overhead fra Spring (proxy method) |
| **Typisk anvendelse** | Når man ønsker fuld lavniveaukontrol | Standardvalg i Spring-applikationer |  

I praksis anbefales det at bruge @Transactional i Spring-applikationer, fordi det giver enklere og mere pålidelig transaktionsstyring.
Men det er vigtigt at forstå den manuelle mekanisme – som i eksemplet ovenfor – da det giver bedre forståelse af, hvad Spring faktisk gør “under motorhjelmen”.



## Aktiviteter
- Check jeres repository kode og identificér eventuelle behov for transaktionsstyring
- Implementér transaktionsstyring, hvis nødventigt

