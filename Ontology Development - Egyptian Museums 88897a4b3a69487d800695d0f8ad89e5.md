# Ontology Development - Egyptian Museums

---

# Introduction:

### Domain and Scope **of Ontology**

Egyptian history spans over 5000 years, from the early civilisation along the Nile to the modern-day republic. With such a rich history, it's no surprise that Egypt is home to numerous museums, ancient monuments and artefacts. The extensive amount of knowledge available on the Egyptian Ministry of Tourism and Antiquities [1] motivated the creation of an ontology-based knowledge representation that is studied and presented in this report with the aim to build intelligent systems that power the development of the tourism industry. Due to the size and time requirements for this project, the ontology produced focuses on museums only. To be specific, it is used to model museums on Egyptian lands, using the MoA’s online documentation.

### Who can use **and maintain** the Ontology

The designed ontology is particularly useful in mapping Egypt’s extensive list of museums with relevant information online that can be accessed by visitors before visiting each site. Both knowledge ontologists looking to represent such an ancient domain of knowledge and antiquities specialists (such as Egyptologists) can work together to further develop and maintain this ontology.

### Existing Ontologies

An online search was conducted to prepare for building the ontology, yielding the following results:

- Museum artefact retrieval framework [2]: An excellent paper that describes an ontology that semantically classifies museum collection. Although it assisted in defining classes in the museum ontology, it was irrelevant to an extent as its architecture focuses only on images of the artefacts.
- Museum Ontology Based Metadata [3]: This ontology served as an initial idea for the museum ontology. Some of the entities were relevant while others were more focused on events. It is noted, however, that the Egyptian museums’ ontology is significantly more complex as the domain historically includes data from a myriad of sources and formats.

---

# Ontology

### Classes

A top-down development process starts with the definition of the most general terms (classes) in the domain and subsequent specialisation of these terms (subclasses). By navigating through the website, and recalling previous working knowledge with the ministry, the following table was constructed to list the 24 classes of the ontology with their axioms and assumptions before creating them in Protege. Class axioms are included in the table and used where appropriate.

| Classes | Subclasses |  |  | Axioms & Assumptions |
| --- | --- | --- | --- | --- |
| Museums |  |  |  | Disjoint Union of Permenant Collections and Temp Exibitions |
|  | Permenant Collections |  |  |  |
|  | Temp Exibitions |  |  |  |
| Ticket |  |  |  |  |
| Person |  |  |  | Union of Worker & Visitor (A worker can also Visit) |
|  | Worker |  |  |  |
|  | Visitor |  |  |  |
|  |  | Egyptians |  |  |
|  |  |  | Egyptian Students |  |
|  |  | Non-Egyptians |  |  |
|  |  | Arab |  | Equivalent to Egyptians because MoA gives same ticket price to both |
| Cultural Information |  |  |  |  |
|  | Descriptive Story Line |  |  |  |
|  |  | Historical Period |  |  |
|  | Listings |  |  |  |
|  | Gallery |  |  |  |
| Location  |  |  |  |  |
|  | Country |  |  |  |
|  |  | City |  |  |
|  |  |  | Street |  |
| Opening Hours |  |  |  |  |
| Building |  |  |  |  |

Figure 1 below provides the hierarchical visualisation of classes.

![Fig 1: Class Hierarchy.](Ontology%20Development%20-%20Egyptian%20Museums%2088897a4b3a69487d800695d0f8ad89e5/classes.png)

Fig 1: Class Hierarchy.

### Properties

The classes alone will not provide enough information to answer important competency questions about the museums. Therefore, we must describe the internal structure of concepts, using properties. Table 2 below has been constructed to define 2 types of properties: 16 Object properties to join classes with each other, and 20 data properties to join them with literal values. For each property in the list, we must determine which class it describes using domains and ranges. The architecture includes object properties that could have been data types (e.g. happenedDuring) where the range classes represent an important entity that we could further dissect and model in the future(e.g. Historical Period). Property axioms and restrictions such as transitive, symmetric and functional types are included in the table.

| Property | Type | Domain | Range | Other Axioms | Assumptions |
| --- | --- | --- | --- | --- | --- |
| buys | Object | Visitor | Ticket | Symmetric | Booking Method Disgarded |
| exists | Object | Museum | Location |  |  |
| inCountry | Object | Location | Country |  | Value: Egypt |
| isPartOf | Object | City | Country |  |  |
| locatedIn | Object | Street | City | Transitive |  |
| foundOnline | Object | Location | Link | Functional | a location is unique on map |
| accessedBy | Object | Museum | Ticket | Functional |  |
| documentedThrough | Object | Permenant Collections | Cultural Information |  | Info used as a class becuase it can be further dissected |
| includedIn | Object | Museum | Listing |  |  |
| describes | Object | Descriptive Story Line | Museum |  |  |
| happenedDuring | Object | Descriptive Story Line | Historical Period |  |  |
| associatedWith | Object | Descriptive Story Line | Gallery |  |  |
| employs | Object | Museum | Worker |  |  |
| worksAt | Object | Worker | Museum | Inverse of employs |  |
| opensDuring | Object | Museum | OpeningHours |  |  |
| has | Object | Museum | Building |  |  |
| hasEmail | Datatype | Visitor | String |  |  |
| hasID | Datatype | Worker | String | Functional |  |
| hasTicketNo | Datatype | Ticket | Integer | Functional |  |
| hasPhoneNo | Datatype | Person | Integer |  |  |
| hasName | Datatype | Person | String | Functional |  |
| hasStartDate | Datatype | Temp Exibitions | Date | Disjoint with hasEndDate |  |
| hasEndDate | Datatype | Temp Exibitions | Date |  |  |
| ticketLink | Datatype | Museum | String |  | URL if available |
| start | Datatype | Historical Period | String | Disjoint with End |  |
| end | Datatype | Historical Period | String |  |  |
| hasInfo | Datatype | Listing | String |  |  |
| dateAwarded | Datatype | Listing | Date |  |  |
| touristCapacity | Datatype | Building | Integer |  |  |
| eventCapacity | Datatype | Building | Integer |  | Capacity of 0 means it is not open for event hires. |
| isAccessible | Datatype | Building | Boolean |  |  |
| hasImages | Datatype | Gallery | Images |  |  |
| duringWeekdays | Datatype | OpeningHours | String | Disjoint with during Weekends | Easier to model as string than using time values |
| duringWeekends | Datatype | OpeningHours | String |  |  |
| hasPrice | Datatype | Ticket | Integer |  |  |
| hasURL | Datatype | Link | String | Functional |  |

Although there can be various implementations of both class and property definitions, the produced ontology is based on the most relevant classes from a historical and logistic perspective. In other words, we are more concerned with classes and properties describing the history and the visit details of the museum. Details such as services are out of this ontology’s scope.

### Graph Representation

To better understand the ontology, Protege’s plugin VOWL was used to visualise the ontology architecture, with classes, object and data properties, class and property axioms included. The resulting visualisation is highlighted below in figure 2.

![Fig 2: Museums Ontology Graph.](Ontology%20Development%20-%20Egyptian%20Museums%2088897a4b3a69487d800695d0f8ad89e5/onto2.png)

Fig 2: Museums Ontology Graph.

### Individuals

49 Different instances of all classes have been created and used to populate the ontology-based model. Fig 3 below displays a snapshot of these individuals. After creating them, object assertions were created where data instances from connected classes were established in Protege. Similarly, data properties of relevant individuals were created to build a consistency, full realisation for the ontology. For object properties, domain and range classes were added, while for data properties, instance values were entered.

![Fig 3: Individuals created.](Ontology%20Development%20-%20Egyptian%20Museums%2088897a4b3a69487d800695d0f8ad89e5/Ind.png)

Fig 3: Individuals created.

### Example Museum: The coptic museum

The coptic museum in Cairo is a famous multi-faceted museum with many collection throughout different periods in Egyptian history. We use it for the propose of illustrating how it was used to instantiate the ontology’s class and properties to represent the respective knowledge available online [4]

Figure 4 highlights the creation of an individual ‘Coptic_Museum’ that belongs to class of Museums on the Egyptian Museums ontology. The individual’s relationships with other classes are created through the following object properties:

1. **inCountry,** specifying the country of location (connecting to Country class instances).
2. **accessed_by,** listing the ticket holders that can access it (connecting to Ticket class instances)
3. **exists,** providing the location (connecting to Location class instances)
4. **employs,** listing all registered workers in the museum (connecting to Worker class instances).

![Fig 4: Coptic Museum Class with Object Properties.](Ontology%20Development%20-%20Egyptian%20Museums%2088897a4b3a69487d800695d0f8ad89e5/coptic_mus.png)

Fig 4: Coptic Museum Class with Object Properties.

Figure 5 highlights the creation of another individual **Coptic_Museum_Story** that belongs to class of **Descriptive_Story_Line** on the Egyptian Museums ontology. The individual’s relationships with other classes are created through the following object properties:

1. **describes,** linking it to the exact museum it is telling the story of (connecting to **Museums** class instances).
2. **associatedwith,**  linking it to the gallery images of this specific museum (connecting to **Gallery** class instances).
3. **happenedDuring,** providing the historical period of the collections inside the museum (connecting to **Historical_Period** class instances).

![Fig 5: Coptic Museum’s Story with Object Properties.](Ontology%20Development%20-%20Egyptian%20Museums%2088897a4b3a69487d800695d0f8ad89e5/coptic_story.png)

Fig 5: Coptic Museum’s Story with Object Properties.

Additionally, the **RDFS:comment** resource was used to provide the full text of the story behind that museum as available online for semantic relevance and clarity [4].

### OWL Statements

This section includes OWL statements created in Turtle syntax. The Turtle syntax is often preferred over RDF/XML as it is more compact and easier to read and write.

1. This statement defines an ontology called "Egyptian Museums Ontology" with a creator of "22206549" and a date of "2023-04-25". The ontology imports several standard ontologies such as RDF, RDF Schema and OWL ontologies using their standard namespaces. Additionally, the statement includes information about the ontology's version, indicating that it is the first version (1.0), and that it is backward-compatible with the previous version (v0.9). It also includes a link to the prior version of the ontology. Turtle's short syntax for RDF predicates is used, where a is a shorthand for the **rdf:type** predicate.

```jsx
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
PREFIX owl: <http://www.w3.org/2002/07/owl#> .
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> .
PREFIX : <http://www.semanticweb.org/22206549/inst0069/cw#> .
<http://www.semanticweb.org/22206549/inst0069/cw>
  a owl:Ontology ;
  rdfs:label "Egyptian Museums Ontology" ;
  dc:creator "22206549" ;
  dc:date "2023-04-25" ;
  owl:imports <http://www.w3.org/1999/02/22-rdf-syntax-ns#> ,
              <http://www.w3.org/2002/07/owl#> ,
              <http://www.w3.org/2000/01/rdf-schema#>
							<http://www.w3.org/2001/XMLSchema#> ;
  owl:versionInfo "Version 1.0" ;
  owl:priorVersion <http://www.semanticweb.org/22206549/inst0069/cw_v0.9> ;
  owl:backwardCompatibleWith <http://www.semanticweb.org/22206549/inst0069/cw_v0.9> .

```

1. In these statements, we define the classes **Museum, Building, Person, Worker, Visitor, and Ticket** using the **owl:Class** statement. We also define two subclasses of Person: Worker and Visitor using the **rdfs:subClassOf** property. The rdfs:label property is used to provide a human-readable label for each class, which can be semantically helpful when working with ontologies.

```jsx
:Museum a owl:Class ;
  rdfs:label "Museum" .

:Building a owl:Class ;
  rdfs:label "Building" .

:Person a owl:Class ;
  rdfs:label "Person" .

:Worker a owl:Class ;
  rdfs:label "Worker" ;
  rdfs:subClassOf :Person .

:Visitor a owl:Class ;
  rdfs:label "Visitor" ;
  rdfs:subClassOf :Person .

:Ticket a owl:Class ;
  rdfs:label "Ticket" .
```

1. This statement defines a property employs that can be used to represent the employment relationship between museums and workers in the ontology. employs is an **owl:ObjectProperty**, which means it relates two individuals or instances in the ontology. **rdfs:domain** specifies the domain of the property, which in this case is **:Museums**. This means that the **employs** property can only be used to relate a museum to a worker. **rdfs:range** specifies the range of the property, which in this case is **:Worker**. This means that the employs property can only be used to relate a museum to an individual who is a worker. **owl:inverseOf** specifies the inverse of the employs property, which in this case is **:worksAt**. This means that if a museum employs a worker, then that worker works at the museum.

```jsx
:employs a owl:ObjectProperty ;
        rdfs:domain  :Museums ;
        rdfs:range   :Worker;
				owl:inverseOf :worksAt .
```

---

# Querying the Museum Knowledge Base

### SPARQL Queries **and The Motivation Behind Them**

The following queries were performed to retrieve instances of the classes in the ontology.

1. Retrieve all Museums, and If available, the employed workers. This can help the ministry overlook specific operations and skills in each museum.

```jsx
SELECT ?museum ?worker
WHERE {
  ?museum a mus:Museums .
  OPTIONAL {
    ?museum mus:employs ?worker .
  }
}
```

1. Retrieve all museums with capacity > 300 (visits). This can help the ministry control traffic and manage museum visits.

```jsx
SELECT ?building ?touristCapacity
WHERE {
  ?building a mus:Building .
  ?building mus:touristCapacity ?capacity .
  FILTER (?capacity > 300)
}
```

1. For each museum that has a listing, creates a statement of this form ?museum mus:listingStatus "listed". This will assist in identifying which museums have earned different awards and listings to help promote them [5].

```jsx
CONSTRUCT {?museum mus:listingStatus "listed".}
WHERE {
?museum a mus:museums.
?museum mus:includedIn mus:Listings.
}
```

---

# Reflections and Future Work

### Limitations

Creating an ontology for old museums can be a challenging task due to several limitations. One of the main limitations is the lack of standardisation in the data models used by museums, especially for old museums that may have been using legacy (mostly manual) systems. This can result in inconsistencies and errors when mapping the data to the ontology.
Another limitation is the difficulty in capturing the complexity and nature of museum objects and their relationships. Museums often have diverse collections with complex interrelationships, making it challenging to create a comprehensive and accurate ontological representation. One way to tackle this is by grouping collections by historical periods as achieved in our ontology.
Moreover, creating an ontology for old museums can be a time-consuming process, requiring extensive domain expertise and knowledge. Additionally, keeping the ontology up-to-date with changes in the museum collection or technology can also be a challenge, however, it creates excellent job opportunities for many egyptologists in the sector that might be struggling with unemployment due to the impact of the pandemic on the tourism sector.

### Strengths

Creating an ontology can help to identify and clarify concepts and relationships within the museum domain, enabling better understanding and communication of museum objects and collections. It can also provide a foundation for developing new applications and services for museum visitors and researchers, such as recommendation systems and semantic search engines.

This can help to enable more efficient and effective sharing of data and knowledge between museums and other cultural heritage institutions.

### Further Development

The Egyptian museum ontology created for old museums may not be easily extensible to other countries’ museums or cultural heritage institutions, which may have different data models and requirements. Despite these limitations, creating an ontology for old museums can still provide significant benefits in terms of data integration, knowledge management, and cultural discovery. Furthermore, it can support the digital services that many governments and organisations are trying to provide in the tourism sector. This model can be extended to include museum services, trips and other types of cultural or historical sites that are all available on the MoA’s website.

---

# References

1. *Ministry of Antiquities* (no date) *Discover Egypt's Monuments - Ministry of Tourism and Antiquities*. Available at: [https://egymonuments.gov.eg/](https://egymonuments.gov.eg/)  (Accessed: April 23, 2023).
2. *An ontology based framework for retrieval of museum artifacts* (2016) *Procedia Computer Science*. Elsevier. Available at: [https://www.sciencedirect.com/science/article/pii/S1877050916300989?ref=pdf_download&fr=RR-2&rr=7b3a0e728ea511a5](https://www.sciencedirect.com/science/article/pii/S1877050916300989?ref=pdf_download&fr=RR-2&rr=7b3a0e728ea511a5)  (Accessed: April 23, 2023).
3. *Museum ontology-based metadata - IEEE Conference publication* (no date). Available at: [https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7439312](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7439312)  (Accessed: April 23, 2023).
4. *The Coptic Museum* (no date) *Discover Egypt's Monuments - Ministry of Tourism and Antiquities*. Available at: [https://egymonuments.gov.eg/en/museums/the-coptic-museum](https://egymonuments.gov.eg/en/museums/the-coptic-museum)  (Accessed: April 24, 2023).
5. *Centre, U.N.E.S.C.O.W.H. (no date) Egyptian Museum in Cairo, UNESCO World Heritage Centre. Available at: [https://whc.unesco.org/en/tentativelists/6511/](https://whc.unesco.org/en/tentativelists/6511/)  (Accessed: April 24, 2023).* 

---