# Test: Mockito + H2

## Beskrivelse

## Forberedelse

## Læringsmål

## Indhold
### Hvad er H2?
H2 er en lille, hurtig, Java-baseret relationel database, der kan køre in-memory (eller som fil) inde i din JVM-proces. Det gør den ideel til hurtige, integrationstests uden ekstern opsætning.  
Fordele ved at benytte H2 i tests:
- Lynhurtig opstart og nedlukning
- Ren database ved hvert test-run
- Ingen lokal serverdatabase at installere/vedligeholde
- Kompatibel med JDBC API (men der er små forskelle i sql syntaks ift f.eks. MySql), se [MySQL vs H2](https://www.geeksforgeeks.org/blogs/mysql-vs-h2/)
  
Vi bruger kun H2 i tests. Produktion/dev skal fortsat køre på den “rigtige” DB (fx MySQL).

### H2 dependency i pom.xml
H2 databasen benyttes ved at inkludere denne dependency i pom.xml 

```xml
<dependency>
   <groupId>com.h2database</groupId>
   <artifactId>h2</artifactId>
   <scope>test</scope>
</dependency>
```

<scope>test</scope> angiver at databasen kun skal være tilgængelig i testmiljøet
Der oprettes automatisk en database ´testdb’ med username = sa og password = ""

## Aktiviteter
