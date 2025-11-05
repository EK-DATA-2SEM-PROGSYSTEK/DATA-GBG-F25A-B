# Java Collections Framework (og Wishlist projekt feedback fortsat)

## Beskrivelse

Vi kigger nærmere på Java Collections Framework og de forskellige typer af Collections, deres egenskaber
samt hvordan man vælger den rette Collection type til en given opgave.

---

## Forberedelse

Læs: 

[Getting to Know the Collection Hierarchy](https://dev.java/learn/api/collections-framework/organization/)


[Using Maps to Store Key Value Pairs](https://dev.java/learn/api/collections-framework/maps/)


---

## Læringsmål

- At kunne anvende Java Collections interfaces og klasser 
(herunder Set, Map, List, HashSet, TreeSet, HashMap og TreeMap)
- At kunne vælge den rette Collection type til en given opgave

  
---

## Indhold

---

 `ArrayList` - one size fits all?

<img src="assets/container.jpg" alt="container" width="500">

---

Egenskaber for en indkøbslist, emaillist?


<img src="assets/shoppinglist.png" alt="emaillist" width="500">

---

<img src="assets/emaillist.png" alt="emaillist" width="500">

---

## [Set](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Set.html)


![Set](assets/set.png)

---

```mermaid
classDiagram
    direction TB

    class Collection {
        <<interface>>
        +add(E)
        +remove(Object)
        +size()
        +iterator()
    }

    class List {
        <<interface>>
        +get(int)
        +set(int, E)
        +add(int, E)
    }

    class Set {
        <<interface>>
        +add(E)
        +contains(Object)
    }



%% Relationships
    Collection <|-- List
    Collection <|-- Set

%% --- Implementations of List ---
    class ArrayList
    class LinkedList


    List <|-- ArrayList
    List <|-- LinkedList
 

%% --- Implementations of Set ---
    class HashSet
    class LinkedHashSet
    class TreeSet

    Set <|-- HashSet
    Set <|-- LinkedHashSet
    Set <|-- TreeSet
```

---


Andre egneskaber for en "collection"...

<img src="assets/dictionary.png" alt="dictionary" width="500">

---

<img src="assets/postnord.png" alt="postbyer" width="900">

---

```mermaid
flowchart LR
    subgraph L[Keys]
        direction TB
        k1["&quot;2200&quot;"]
        k2["&quot;2100&quot;"]
        k3["&quot;2300&quot;"]
    end

    subgraph R[Values]
        direction TB
        v1["&quot;København N&quot;"]
        v2["&quot;København Ø&quot;"]
        v3["&quot;København S&quot;"]
    end

    k1 --> v1
    k2 --> v2
    k3 --> v3
```

---

## [Map](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Map.html)

![Map](assets/map.png)

---

```mermaid
    classDiagram
    direction TB

    class Map {
        <<interface>>
        +put(K, V)
        +get(Object)
        +remove(Object)
        +keySet()
        +values()
    }

%% --- Implementations of Map ---
    class HashMap
    class LinkedHashMap
    class TreeMap

    Map <|-- HashMap
    Map <|-- LinkedHashMap
    Map <|-- TreeMap
```

---

### Collections opsummering

- **List**: **Ordnet sekvens**, tillader duplikater, har **indeks**.
- **Set**: Mængde af **unikke** elementer, ingen indeks, orden afhænger af implementering.
- **Map**: **Nøgle → værdi-opslag**; nøgler er unikke, værdier kan gentage; ikke en Collection, men har views (keySet, values, entrySet).


## Aktiviteter

### Opgave

[Opgave: Tour de France](Tour-de-France-2025-Øvelse.pdf)