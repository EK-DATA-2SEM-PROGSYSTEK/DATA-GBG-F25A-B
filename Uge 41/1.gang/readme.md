# Test: Mockito + H2

## Beskrivelse

## Forberedelse

## Læringsmål

## Indhold
### Hvad er H2?
H2 er en lille, hurtig, Java-baseret relationel database, der kan køre in-memory (eller som fil) inde i din JVM-proces. Det gør den ideel til hurtige, deterministiske tests uden ekstern opsætning.
Hvorfor H2 i tests?
- Lynhurtig opstart og nedlukning
- Ren database ved hvert test-run
- Ingen lokal serverdatabase at installere/vedligeholde
- Vi bruger H2 kun i tests. Produktion/dev kan fortsat køre på din “rigtige” DB (fx MySQL).
- Kompatibel med JDBC API (men der er små forskelle i sql syntaks ift f.eks. MySql), se [MySQL vs H2](https://www.geeksforgeeks.org/blogs/mysql-vs-h2/)


## Aktiviteter
