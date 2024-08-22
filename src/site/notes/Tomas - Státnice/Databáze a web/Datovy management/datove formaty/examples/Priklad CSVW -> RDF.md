---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/datovy-management/datove-formaty/examples/priklad-csvw-rdf/","tags":["tomas","datovy_management","databaze_a_web"],"noteIcon":""}
---

> [!NOTE] ChatGPT
> Vygenerováno pomocí ChatGPT na základě přednášek od Klimka
### **Example CSV File (books.csv)**

```csv
id,title,author,published_date,price
1,The Catcher in the Rye,J.D. Salinger,1951-07-16,8.99
2,To Kill a Mockingbird,Harper Lee,1960-07-11,7.99
3,1984,George Orwell,1949-06-08,6.99
```

### **Step 1: Define Metadata Using JSON-LD**

This metadata file describes the structure of the `books.csv` file and how to transform it into RDF.

```json
{
  "@context": "http://www.w3.org/ns/csvw",
  "url": "books.csv",
  "tableSchema": {
    "columns": [
      {
        "name": "id",
        "titles": "id",
        "datatype": "integer"
      },
      {
        "name": "title",
        "titles": "title",
        "datatype": "string"
      },
      {
        "name": "author",
        "titles": "author",
        "datatype": "string"
      },
      {
        "name": "published_date",
        "titles": "published_date",
        "datatype": "date"
      },
      {
        "name": "price",
        "titles": "price",
        "datatype": "decimal"
      }
    ],
    "primaryKey": "id"
  },
  "rdfs:label": "Books",
  "rdfs:comment": "A list of books and their details",
  "dc:creator": "Tomas"
}
```

#### **Important Parts Highlighted:**
- **@context**: Defines the context for CSVW metadata, ensuring that the CSV file is interpreted correctly according to the CSVW standard.
- **url**: Points to the `books.csv` file.
- **tableSchema**: Describes the schema of the CSV file, including the columns (`name`, `titles`, `datatype`), which are crucial for mapping to RDF.
- **primaryKey**: Specifies the primary key column (`id`), which uniquely identifies each row.
- **rdfs:label** and **rdfs:comment**: Provide additional metadata about the dataset, useful for understanding the dataset's purpose and contents.

### **Step 2: Annotate the CSV and Prepare for RDF Transformation**

Each column in the CSV file is annotated to specify how it should be transformed into RDF triples.

- **id**: Maps to a unique identifier (URI) for each book.
- **title**: Maps to an RDF property representing the book's title.
- **author**: Maps to an RDF property representing the book's author.
- **published_date**: Maps to a date property in RDF.
- **price**: Maps to a decimal value representing the book's price.

### **Step 3: Transformation to RDF**

Using the metadata, the CSV file can be automatically converted to RDF. Below is an example of the RDF triples generated for the first row in the CSV file.

```turtle
@prefix ex: <http://example.org/books/> .
@prefix schema: <http://schema.org/> .

ex:book1 a schema:Book ;
  schema:name "The Catcher in the Rye" ;
  schema:author "J.D. Salinger" ;
  schema:datePublished "1951-07-16"^^xsd:date ;
  schema:price "8.99"^^xsd:decimal .
```

#### **Important Parts Highlighted:**
- **@prefix**: Defines the prefixes for URIs used in the RDF data.
- **ex:book1**: Represents the subject (a unique identifier for each book) in the RDF triple.
- **schema:name**, **schema:author**, **schema:datePublished**, **schema:price**: These predicates describe properties of the book, mapped directly from the CSV columns.
- **^^xsd:date** and **^^xsd:decimal**: Indicate the data types for the published date and price, ensuring correct interpretation of these values in RDF.

### **Best Practices Reinforced in the Example:**

1. **Descriptive Headers**: The CSV file uses clear, descriptive headers (e.g., `title`, `author`), which are easily mapped to RDF properties.
2. **Data Types**: Data types are explicitly defined in the metadata (`date`, `decimal`), ensuring the correct conversion to RDF.
3. **Primary Key**: The `id` column is designated as the primary key, ensuring each RDF subject is uniquely identified.

### **Step 4: Custom Conversion (Optional)**

You could customize the RDF URIs using templates. For instance:

```json
{
  "columns": [
    {
      "name": "id",
      "titles": "id",
      "valueUrl": "http://example.org/books/{id}"
    },
    ...
  ]
}
```

This would result in URIs like `http://example.org/books/1` for each book, making the RDF data more meaningful and accessible.