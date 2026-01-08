# NoSQL Database Analysis – FlexiMart

## Section A: Limitations of RDBMS (150 words)

Relational databases like MySQL or PostgreSQL work well when data has a fixed and well-defined structure. However, FlexiMart’s expanding product catalog introduces challenges that are difficult to manage in an RDBMS.

Different product types have different attributes. For example, laptops require fields such as RAM, processor, and storage, while shoes require size, color, and material. In an RDBMS, this would require either adding many nullable columns or creating multiple product-specific tables, both of which increase complexity.

Frequent schema changes are another issue. Each time a new product type is introduced, the database schema must be altered, which can be time-consuming and risky in production systems.

Additionally, storing customer reviews as nested data is inefficient in RDBMS. Reviews would require separate tables and complex joins, making queries slower and harder to maintain.

---

## Section B: NoSQL Benefits (150 words)

MongoDB solves these challenges by using a flexible, document-based schema. Each product can be stored as a JSON-like document, allowing different attributes for different product types without modifying the overall database structure. This makes it easy to add new product categories with unique fields.

Embedded documents are another key advantage. Customer reviews can be stored directly inside the product document as nested arrays. This improves read performance and simplifies queries, as product and review data can be retrieved together without joins.

MongoDB also supports horizontal scalability through sharding. As FlexiMart’s product catalog and traffic grow, data can be distributed across multiple servers, ensuring better performance and availability. This makes MongoDB well-suited for handling large volumes of diverse and rapidly changing product data.

---

## Section C: Trade-offs (100 words)

One disadvantage of MongoDB compared to MySQL is weaker support for complex transactions. While MongoDB supports transactions, relational databases still handle multi-table transactional consistency more efficiently.

Another drawback is data redundancy. Since MongoDB often uses embedded documents, some data may be duplicated across documents. This can increase storage usage and make updates more complex if the same data needs to be changed in multiple places.
