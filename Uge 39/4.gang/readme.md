
# Turistguide del 3, normalisering, SQL DDL

## Beskrivelse

Vi ser hvordan vi kan strukturere en database og organiserer data i tabeller på en måde, 
der reducerer redundans (gentagne data) og forbedrer dataintegritet. 
Det gør vi ved at kigge på 1., 2. og 3. normalform.

Vi ser også på hvordan vi kan anvende SQL DDL (Data Definition Language) til at oprette databaser og tabeller.

## Forberedelse

Se videoer:

[Normalization: first, second and third form](https://www.linkedin.com/learning-login/share?account=36836804&forceAccount=false&redirect=https%3A%2F%2Fwww.linkedin.com%2Flearning%2Fprogramming-foundations-databases-2%2Fnormalization-2%3Ftrk%3Dshare_video_url%26shareId%3DIsTl7CEuSX6lgNbtVl3%252Ftg%253D%253D)

[DDL](https://www.linkedin.com/learning-login/share?account=36836804&forceAccount=false&redirect=https%3A%2F%2Fwww.linkedin.com%2Flearning%2Fprogramming-foundations-databases-2%2Fcreating-a-database%3Ftrk%3Dshare_video_url%26shareId%3DUIS%252FcAcMQxmgB6iVaSU0bg%253D%253D)

## Læringsmål

- At kunne beskrive 1., 2. og 3. normalform.
- At kunne normalisere en database til 3. normalform.
- At kunne anvende SQL DDL til at oprette databaser og tabeller.

## Indhold

---

### Normalisering

#### Formålet

Det overordnede formål med normalisering er at organisere data i en database på en måde, 
der reducerer redundans og forbedrer dataintegritet.

Det gøres ved at opdele data i mindre, relaterede tabeller og definere relationer mellem dem.

Data integritet betyder, at data i et system er korrekte, konsistente og pålidelige når
de bliver oprettet, opdateret, lagret og anvendes.

---

#### Normalformer

Først Normalform (1NF) - Atomiske værdier
- Alle attributter (kolonner) indeholder kun atomiske værdier (ikke lister eller gentagelser).

Andet Normalform (2NF) - Fuld funktionel afhængighed
- Kræver først 1NF.
- Alle ikke-nøgleattributter skal være fuldt afhængige af hele komposit primærnøglen (ikke kun en del af den).

Tredje Normalform (3NF) - Ingen transitive afhængigheder
- Kræver først 2NF.
-  Ingen ikke-nøgleattributter må være afhængige af en anden ikke-nøgleattribut

---

1NF?

| CourseID (PK) | CourseName        | LecturerEmail         | LecturerName | Students                   |
|---------------|-------------------|-----------------------|--------------|----------------------------|
| 101           | Databaser         | jensen@uni.example    | Jensen       | S1001, S1002, S1003        |
| 102           | Programming       | hansen@uni.example    | Hansen       | S1004, S1005               |
| 103           | Web Development   | smith@uni.example     | Smith        | S1001, S1006               |

---

1NF? 2NF?

| CourseID (PK) | StudentNo (PK) | CourseName      | LecturerEmail       | LecturerName |
|---------------|----------------|-----------------|---------------------|--------------|
| 101           | S1001          | Databaser       | jensen@uni.example  | Jensen       |
| 101           | S1002          | Databaser       | jensen@uni.example  | Jensen       |
| 101           | S1003          | Databaser       | jensen@uni.example  | Jensen       |
| 102           | S1004          | Programming     | hansen@uni.example  | Hansen       |
| 102           | S1005          | Programming     | hansen@uni.example  | Hansen       |
| 103           | S1001          | Web Development | smith@uni.example   | Smith        |
| 103           | S1006          | Web Development | smith@uni.example   | Smith        |

---

2NF? 3NF?

Courses

| CourseID (PK) | CourseName      | LecturerEmail       | LecturerName |
|---------------|-----------------|---------------------|--------------|
| 101           | Databaser       | jensen@uni.example  | Jensen       |
| 102           | Programming     | hansen@uni.example  | Hansen       |
| 103           | Web Development | smith@uni.example   | Smith        |


Enrollments

| CourseID (PK) | StudentNo (PK) |
|---------------|----------------|
| 101           | S1001          |
| 101           | S1002          |
| 101           | S1003          |
| 102           | S1004          |
| 102           | S1005          |
| 103           | S1001          |
| 103           | S1006          |

---

3NF?

Lecturers

| LecturerEmail (PK) | LecturerName |
|--------------------|--------------|
| jensen@uni.example | Jensen       |
| hansen@uni.example | Hansen       |
| smith@uni.example  | Smith        |


Courses

| CourseID (PK) | CourseName      | LecturerEmail (FK) |
|---------------|-----------------|--------------------|
| 101           | Databaser       | jensen@uni.example |
| 102           | Programming     | hansen@uni.example |
| 103           | Web Development | smith@uni.example  |


Enrollments

| CourseID (PK) | StudentNo (PK) |
|---------------|----------------|
| 101           | S1001          |
| 101           | S1002          |
| 101           | S1003          |
| 102           | S1004          |
| 102           | S1005          |
| 103           | S1001          |
| 103           | S1006          |


---

#### Opgave: Normalisering

[Opgave: Normalisering](opgave-normalisering.md)

---

### SQL DDL


---


## Aktiviteter


#### Opgave: Normalisering
(Opgave: Normalisering)[opgave-normalisering.md]

