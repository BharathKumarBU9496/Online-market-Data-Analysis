# Online-market-Data-Analysis
Online Marketplace Data Warehouse Management &amp; Business Analytics.

**INTRODUCTION**

Effectively analyzing customer behavior product performance and operational efficiency is critical in the rapidly changing world of global e-commerce. Using MySQL’s powerful features to meet these analytical needs is the main responsibility of my job as a database designer hired to plan and oversee an analytics data warehouse for a top online marketplace. This entails creating a scalable dependable and easily accessible data storage system that facilitates the execution of complex queries and real-time data processing. (1Md Mostafizur Rahman, July-2024).
MySQL is the foundation of our data architecture because of its well-known performance and adaptability. For the data warehouse to manage the massive amounts of data produced every day by millions of users worldwide high data throughput comprehensive query optimization and sophisticated indexing techniques are essential. Furthermore, it is essential to guarantee data security and integrity because the warehouse must adhere to global data protection laws while offering precise and useful insights. (Panwar, March 2024).

A dimensional data model which breaks down complicated data into easily analyzed formats is incorporated into the warehouses design. Making strategic business decisions requires effective data aggregation and reporting which this model makes possible. MySQL’s partitioning data replication and event scheduling features improve performance and guarantee constant data availability even during periods of high load. (1Md Mostafizur Rahman, July-2024).

To further optimize the system stored procedures and custom SQL scripts are used to automate repetitive tasks and optimize data transformation processes allowing for more accurate data analysis and quicker response times. In addition to anticipating consumer preferences and market trends the marketplace can increase revenue growth and operational efficiency with this customized database solution.
You can click the link below to view all of the queries I used for this warehouse project.


**CHAPTER 1: DATA INTEGRATION IN DATABASE DESIGN.**

1.1: Define three concrete objectives on Online Marketplace Data Warehouse.

Objective 1: Which vendors make the biggest contributions to profitability and which products yield the highest profit?
Objective 2: What are consumers buying patterns? preferred product categories average order value and order frequency?
Objective 3: How do sales and profitability relate to which products get the most reviews and the highest ratings?

**1.2: Create a Conceptual Entity-Relationship (ER) Diagram Using Chen Notation.**

**Designing the ER Diagram: Determining the primary entities and their connections in accordance with the specified criteria.
Entities: Attributes**
1.	Products: Attributes include Product_ID, Name, Description, Category.
2.	Vendors: Attributes include Vendor_ID, Name, Contact_Info, Rating.
3.	Customers: Attributes include Customer_ID, Type (member/guest), Name, Phone, Shopping (Online/Retail) .
4.	Orders: Attributes include Order_ID, Date, Shopper_ID, Product_ID, Quantity, Price, Status.
5.	Reviews: Attributes include Review_ID, Product_ID, Shopper_ID, Rating, Time spent on site, Comment.
6.	Charges: Attributes include Charges, Order_ID, Delivery charges, Return Charges, Amount.
7.	Revenues: Attributes include Revenue_ID, Order_ID, Profit.




**Relationships:**
**1. Orders to Customers**
•	Relationship Name: Likely "Places"
•	Cardinality: One-to-Many
•	Participation: Although a single Customer may place multiple orders or only one order is placed at a time.

**2. Orders to Order_Products (Join Table)**
•	Relationship Name: Typically, "Contains"
•	Cardinality: One-to-Many
•	Participation: Multiple products may be included in each order as indicated by the Order_Products join table. A Many-to-Many relationship between Orders and Products is represented by the join table itself. 

**3. Order_Products to Products**
•	Relationship Name: Part of "Contains"
•	Cardinality: Many-to-One
•	Participation: One product is linked to each entry in the Order_Products table. The other half of the Many-to-Many relationship between Orders and Products is reflected in this.

**4. Revenues to Orders**
•	Relationship Name: "Generates"
•	Cardinality: One-to-One
•	Participation: There is only one revenue record for every order and there is only one order associated with each revenue record.

**5. Costs to Orders**
•	Relationship Name: "Incurs"
•	Cardinality: One-to-One
•	Participation: Orders have costs and each cost record is associated with a single order. If an order allows for the separate recording of several cost types this could also be one-to-many.

**6. Reviews to Products**
•	Relationship Name: "Reviews"
•	Cardinality: One-to-Many
•	Participation: Although a single product may be the subject of several reviews each review is specific to that one product.

**7. Reviews to Customers**
•	Relationship Name: "Writes"
•	Cardinality: One-to-Many
•	Participation: Although each review is written by a single customer each customer may write more than one review. 

**8. Products to Product_Vendors (Join Table)**
•	Relationship Name: "Offers"
•	Cardinality: Many-to-Many
•	Participation: As indicated by the Product_Vendors join table each vendor may offer more than one product and each product may be offered by multiple vendors.

**9. Product_Vendors to Vendors**
•	Relationship Name: Part of "Offers"
•	Cardinality: Many-to-One
•	Participation: A single vendor is linked to each entry in the Product_Vendors join table. The other half of the Many-to-Many relationship between vendors and products is reflected in this.


**1.3: Normalize the Schema and Creating a Physical ER Diagram**

1.	All attributes are fully dependent on their primary keys and all tables’ products, vendors, shoppers, reviews, costs and revenues are normalized up to 3NF. 
2.	Product_ID Quantity and Price are all directly included in the Orders table which may cause normalization problems. So, to follow 3NF I should handle the Many-to-Many relationship between Orders and Products using the Order_Products join table. 
3.	Order_Products: Adhering to 3NF this join table is appropriately structured to manage the Many-to-Many relationship.
4.	Product_Vendors join table ensures that all non-key attributes (like price) rely only on the composite key (Product_ID Vendor_ID) eliminating redundancy and normalizing the Products to Product_Vendors relationship up to 3NF. The Many-to-Many relationship between Products and Vendors was managed by the join table which permits multiple vendors to offer the same product and multiple products to be offered by the same vendor without redundancy or duplication.

 ![image](https://github.com/user-attachments/assets/3cbb8c66-198e-4f30-8aed-f05ae4462cd2)

Figure 1: Physical ER-Diagram


**1.4: Explaining Design Choices. Data Constraints and Comprehensive Data Integration.**
Normalization: To ensure data integrity and remove redundancy the schema is designed in 3NF. Each attribute depends on its primary key to function.
Join tables
•	Scalability for orders with multiple products is ensured by Order_Products which manages the Many-to-Many relationship between Orders and Products. 
•	Product_Vendors encapsulates the mutually beneficial relationship between vendors and products.
One-to-many-relationships
•	Orders to Customers guarantees that each customer can place more than one order. 
•	Reviews to Shoppers and Reviews to Products let customers and products be linked to more than one review but each review stays distinct.
One-to-one-relationships
•	Accurate monitoring of revenue and cost metrics for every order is guaranteed by Revenues to Orders and Costs to Orders.
Mandatory-relationships
•	To ensure full participation solid lines are used in all relationships like Every revenue must be linked to an order and every order must have a shopper.
Data Constraints
•	Referential integrity is maintained by every foreign key. 
•	Data accuracy is ensured by checks and constraints such as NOT NULL.
The data warehouse is optimized for integrity and performance thanks to this structure which strikes a balance between normalization scalability and analytical requirements and this data warehouse contains all the requiring data.

**1.5: MySQL Warehouse Implementation in workbench**

All tables have been created in accordance with the specified schema relationships have been established using primary and foreign keys and constraints such as NOT NULL UNIQUE and data type checks have been applied. The data warehouse has been successfully implemented in MySQL. Incoming reviews are validated using a BEFORE INSERT trigger which makes sure all ratings fall within the acceptable range of 1 to 5. To graphically depict the relationships and schema the ER diagram was also made.











**•	MySQL Customers table Creation.**

![image](https://github.com/user-attachments/assets/c0f17015-7603-4a57-80cf-7de8947f5aa4)

Figure 2: Customers table creation in MySQL.


•	MySQL Order Products table Creation.

![image](https://github.com/user-attachments/assets/3ee0466e-25e7-4627-8974-f21a5962bdc8)

Figure 3: Order Products table creation in MySQL.


•	MySQL revenues table creation.

 ![image](https://github.com/user-attachments/assets/dfb9a261-631e-40bc-a407-77cdb0b902dc)
 
Figure 4: Revenues table creation in MySQL.

•	MySQL revenues table foreign key relationship creation with order table.

![image](https://github.com/user-attachments/assets/c4e6d64e-cc39-49a0-a693-312388931a3b)

Figure 5: Revenue table foreign key creation with order table.


**•	ER Diagram Generated by MySQL after creating all tables with constraints using database and reverse engineering.**

![image](https://github.com/user-attachments/assets/812a15a0-e485-436a-9952-c3307b7ab124)

Figure 6: MySQL generated ER diagram.



**CHAPTER 2: PERFORMANCE OPTIMIZATION WITH SQL AND PYTHON.**

**2.1: Populating the Database with the help of python.**
**1.	Setting up Database connection:**
•	Used the MySQL_Connector library to connect to MySQL database
•	Ensure the correct credentials (host, user, password, database) are configured.

 ![image](https://github.com/user-attachments/assets/e44f80d7-d8e9-4768-9c63-8b27271a5fe1)
 
Code 1: Code connects from python to MySQL.

**2.	Generate data with faker: Used Faker library to generate Random but realistic data.**
 ![image](https://github.com/user-attachments/assets/f1504d2a-6777-405e-8d82-74b4f83533eb)
 
Code 2: Populating Products and Vendors Tables.

 ![image](https://github.com/user-attachments/assets/57dbd69b-5417-4d87-b4cf-9f8eac4af2db)
 
Code 3: Populates Customers, Orders, Reviews Tables.

 ![image](https://github.com/user-attachments/assets/60a51184-340a-4733-aa52-cc7c89f46336)
 
Code 4: Populates Charges Table.

 ![image](https://github.com/user-attachments/assets/2171b31b-2a87-4106-b98b-ecb2c0d681b1)
 
Code 5: Populate Revenues Table.

**3.	Output after Inserting data into tables:**

 ![image](https://github.com/user-attachments/assets/66f8c67d-ab3b-4c2d-82ee-810e821f231c)
 
Code 6: Output When Tables are Populated.

I created a Python script that effectively fills the database with the given data. Data about Products, orders, vendors, customers, reviews, costs, revenues and related relationships are dynamically inserted by the script. And I run that script through CMD (Command Prompt). A direct link to the script is also included for convenience 



**2.2: Develop a series of SQL queries for Optimized Performance.**
Objective 1: Which vendors make the biggest contributions to profitability and which products yield the highest profit?
**Query 1.1: Uses the linked orders and products to determine which ten vendors are making the most profit.**

 ![image](https://github.com/user-attachments/assets/35cf922b-a64b-4a8f-aa71-6a06b7b70daa)
 
Query 1: Top Vendors by Profit.

 ![image](https://github.com/user-attachments/assets/b75e781c-183a-4649-9b13-7c62094e3e78)
 
Output 1: For Query 1.

Query 1.2: Reveals the top ten products making the most money.

![image](https://github.com/user-attachments/assets/148e5f18-45b9-45ff-bcf6-c3f374ca92a2)

Query 2: Top Products by Profit.

 ![image](https://github.com/user-attachments/assets/5b681c49-7924-48b8-8d40-ec2dbb811240)
 
Output 2: For Query 2.

**Objective 2: What are consumers buying patterns? preferred product categories average order value and order frequency?**
Query 2.1: Draws attention to the product categories that are most frequently bought.

 ![image](https://github.com/user-attachments/assets/4ba2cb08-761c-48cf-a5db-b09121abc201)
 
Query 3: Preferred Product Categories.

 ![image](https://github.com/user-attachments/assets/b75996b7-0716-49bf-880f-8aad721f998f)
 
Output 3: For Query 3.

Query 2.2: Determines the average amount spent by members on each order in comparison to guests.

 ![image](https://github.com/user-attachments/assets/c2e4e783-391d-44b5-a41e-6db3c51e032a)
 
Query 4: Average Order Value by Customer Type.

![image](https://github.com/user-attachments/assets/5a9afd08-0a7c-44e4-8a22-26e8fe439980)

Output 4: For Query 4.

Query 2.3: Establishes the frequency of orders placed by members and guests. 

 ![image](https://github.com/user-attachments/assets/5c734ef7-d1eb-4fcf-9570-1268ecbb477d)
 
Query 5: Order Frequency by Customer Type.

![image](https://github.com/user-attachments/assets/b8633edb-20b0-4c21-9b57-6e081f978170) 

Output 5: For Query 5.



**Objective 3: How do sales and profitability relate to which products get the most reviews and the highest ratings?**
Query 3.1: Enumerates the top ten products based on average ratings and the number of reviews.

 ![image](https://github.com/user-attachments/assets/da352247-6feb-4119-802e-f9f67decb170)
 
Query 6: Products with Most Reviews and Ratings.

![image](https://github.com/user-attachments/assets/325e6b65-412a-45ff-9a0c-d1924fb9325c)

Output 6: For Query 6.

Query 3.2: Examines the top ten products sales volume overall profit and number of reviews.

 ![image](https://github.com/user-attachments/assets/fac19aa8-9c91-4d2c-895e-68f3031a39c5)
 
 
Query 7: Correlation of Sales and Profit with Reviews.

 ![image](https://github.com/user-attachments/assets/e1e493d9-98aa-4cd5-a623-f09b73fd6004)
 
Output 7: For Query 7.

Query 3.3: Once a new order is added automatically determines and adds the profit to the Revenues table.

 ![image](https://github.com/user-attachments/assets/ea11fe90-5cbe-4316-8963-382efa74b738)
 
Query 8: Automatically Update Revenues when a New Order is Inserted.






Objective 4: Which customers are the biggest contributors to sales and how often do they order and what do they buy?

Query 4.1: Sorts and ranks clients with over 1000 in revenue.

 ![image](https://github.com/user-attachments/assets/4d7cffcd-4714-487d-9086-a60b72ae8001)
 
Query 9: Identify Customers with the Highest Revenue Contribution.

 ![image](https://github.com/user-attachments/assets/f399297a-f126-49c1-8bfd-7bf576d85cf6)
 
Output 9: For Query 9.


Query 4.2: Counts the total number of orders that each customer has placed.

 ![image](https://github.com/user-attachments/assets/a2d27dfe-4db6-47a5-a087-ce74495a2af2)
 
Query 10: Analyze Order frequency by Customer.


![image](https://github.com/user-attachments/assets/b92fe203-cc3d-4ea1-bafb-71614b149cc5)

Output 10: For query 10.

Query 4.3: Separates clients according to whether they prefer to shop online or in-store.

 ![image](https://github.com/user-attachments/assets/1ef47b8c-4daa-4b24-8c3b-4ec20486e981)
 
Query 11: Determine Preferred Shopping Method.

![image](https://github.com/user-attachments/assets/3bb9d2e3-05ca-47bb-942b-c9c4c11bb78c)

![image](https://github.com/user-attachments/assets/2ccc0620-7827-4b8a-b4c9-fd5a2b5d0e35)

Output 11: For Query 11.


Query 4.4: Uses a window function to rank customers according to their overall revenue contribution.

 ![image](https://github.com/user-attachments/assets/1fd33eb4-fb4f-462f-bf94-ac2f79170f46)
 
Query 12: Rank Customers by Revenue Using Window Functions.

 ![image](https://github.com/user-attachments/assets/cc0b0146-84a1-4fc8-9ab8-32bf2b62f407)
 
Output 12: For Query 12.

Objective 4.5: Combines information from regular customers and top revenue contributors using a UNION ALL.

 ![image](https://github.com/user-attachments/assets/baefe6fd-0a57-4fce-ae39-b61ecd288560)
 
Query 13: Combine Insights Using a set operation.

 ![image](https://github.com/user-attachments/assets/acaf91a8-ec3e-4c46-a556-707def1a1658)
 
Output 13: For Query 13.




**2.3: Create a stored procedure “monthly report” that expects a month value as a parameter.**
This query gives monthly report of product sales and customers Total revenue, Total cost, and Profit.

 ![image](https://github.com/user-attachments/assets/1db3d271-9541-40d5-9943-7908bffe38c4)
 
Query 14: Monthly Report Output.

 ![image](https://github.com/user-attachments/assets/0791fcef-2ea1-404c-8628-a01fa5fcd731)
 
Output 14: For Query 14.

**2.4: Proposal for Optimizing New Customer and Vendor Data Insertion.**

1.	By adding Recommendations Entity: Tracking personalized product suggestions for customers to buy.
2.	Adding Interaction logs Entity: Logs customer actions like Views, Clicks, Likes.
3.	Linking Recommendation to customers: which matches suggestions to customer preferences.
4.	Connect Interaction logs to Products: Which captures specific customer interactions.
5.	Utilizing Existing Orders and Products: Analyzing purchases for strongest recommendations.
6.	Customer value: which satisfied with tailored experiences and time saving.
7.	Vendor Value: which increases visibility, sales, feedback and market insights.

**CHAPTER 3: ENSURING CONSISTENCY, SCALABILITY AND FLEXIBILITY.**

**3.1: Advanced SQL Query Optimization Techniques: A Performance Analysis.**

Performance Analysis: The total profit per customer is calculated by combining data and performing multiple JOIN operations. Database engine efficiency indexing and data volume are some of the variables that affect execution time (Mancini, June-2022). The following query which determines the top 10 clients based on their overall revenue contribution will be examined. 

 ![image](https://github.com/user-attachments/assets/b7a0c758-0432-486c-971e-e711e4e46b8e)
 
Query 15: Highest revenue contribution by customers.

 ![image](https://github.com/user-attachments/assets/99382004-3911-47fe-b3d4-5b9d449f0f30)
 
Output 15: For Query 15.

**Optimization strategies:**
1.	Indexing
•	Order_ID in Revenues and Orders and Customer_ID in Orders and Customers are examples of foreign key columns that should be indexed in order to speed up JOIN operations.
•	Make composite indexes on columns that are frequently used together in queries like Order_ID and Customer_ID.
2.	Query Refactoring
•	Utilize subqueries to minimize the amount of data processed by shrinking the dataset size prior to joins.
•	Common Table Expressions (CTEs): Use CTEs to simplify complicated queries into smaller easier-to-understand chunks improving readability and efficiency.
Database Configuration:
•	To give the optimizer precise data distribution information and improve execution plans update database statistics on a regular basis.
•	Partitioning: By enabling the database to scan only pertinent partitions partitioning large tables can enhance query performance.
Impact of Data Growth
If query performance is not adequately controlled it may deteriorate as database size grows. A tenfold increase in data volume for example may result in noticeably longer execution times because of:
•	Increased I/O Operations: Execution of queries is slowed down by larger datasets which necessitate more disk reads and writes.
•	Memory Limitations: More disk swapping may occur if there is not enough memory to manage bigger datasets.
•	Ineffective Execution Plans: The query optimizer may select less-than-ideal plans for bigger datasets if proper optimization is not done.
In order to optimize join operations for large datasets a study called Efficient Massively Parallel Join Optimization for Large Queries examines the problems and solutions. According to the study conventional optimization methods may not be sufficient as the volume of data and number of tables rises therefore requiring sophisticated algorithms to preserve performance (Mancini, June-2022).

**3.2: ACID Properties in Relational Databases like MySQL**

To ensure the dependability integrity and performance of the database systems it is essential to protect the ACID properties (Atomicity Consistency Isolation and Durability) in my SQL-based database project for an online marketplace (Chittayasothorn, June-2022).
1.	Atomicity: 

Atomicity guarantees that either all or none of the changes are committed for processes like order placement which update the Orders Order_Products and possibly Products tables as a result of stock adjustments. This guarantees that every step of a transaction is finished together and avoids situations where an order is placed without using up all of the stock. 
2.	Consistency: 

Consistency is essential when it comes to the relationships in your database such as the Many-to-Many relationship between Orders and Products via the Order_Products join table. Referential integrity is maintained throughout the system by the databases enforcement of the rule that no order or product record can exist without matching entries in their linked tables. 
3.	Isolation: 

The concurrent nature of transactions many users placing orders or writing reviews at the same time means that isolation keeps these actions from interfering with one another. For example, it prevents conflicts and guarantees that each transaction is handled independently by making sure that two customers cannot buy more stock of a product than is available at the same time. 
4.	Durability: 

Once committed a transaction stay in the system indefinitely such as when recording revenues and costs related to each order. In the event that the system malfunctions after an order have been placed the orders specifics along with the related expenses and income are saved and recoverable. 
In order to guarantee data integrity, avoid data anomalies and offer a dependable and stable user experience your SQL database design with its structured relationships and transactional requirements significantly depends on maintaining ACID properties. To successfully maintain these properties in the database system for my project it is practical to define stringent schema constraints and optimize transaction isolation levels.



**3.3: Applying the CAP Theorem to Marketplace Analytics Data Warehouses.**

In the scenario of an online shopping marketplace with relationships as defined in my project, here’s how the CAP Theorem applies:
1.	Consistency: 

For crucial relationships like orders to customers and products to vendors to be accurate my data model places a high priority on consistency. Data trustworthiness is crucial for financial transactions and customer satisfaction and SQLs properties support this by preserving transaction integrity and dependable reporting. 
2.	Availability: 

Due to their lack of inherent fault tolerance in distributed systems SQL databases prioritize consistency at the expense of availability. Database replication clustering and failover mechanisms are some of the techniques used to improve availability. These techniques help keep the system running albeit occasionally at a lower performance during server failures or network partitions. 
3.	Partition Tolerance: 
Strict partition tolerance is difficult to implement in a SQL database environment because of its focus on consistency. Redundancy and the use of geographically dispersed clusters or distributed SQL databases however can somewhat improve partition tolerance. (Francesc D. Mu˜ noz-Esco´ ı1, 2017).

By using the CAP Theorem in my SQL-based project I give availability and consistency top priority which is essential for preserving transactional integrity and improving the user experience in e-commerce. Strategic database architecture guarantees that I optimize these components to support my unique business needs and processes even though SQL databases might not have perfect partition tolerance. My strategy basically aims to strike the ideal balance between availability and consistency with careful system design to improve partition tolerance as necessary.






**3.4: A Case study on Data warehouses for e-commerce environments.**

Il-Yeol Song and Kelly LeVan-Shultz’s paper Data Warehouse Design for E-Commerce Environments presents a noteworthy case study that highlights the deployment of an analytical data warehouse in an e-commerce setting.
Technology Used in Data Warehouse
With an emphasis on the use of dimensional modeling techniques like star and snowflake schemas to effectively handle and analyze enormous volumes of transactional data the study covers the design of data warehouses for e-commerce environments. The authors data warehouse bus architecture integrates multiple data marts to provide comprehensive analytical capabilities across the e-commerce platforms various aspects. 

**Reasons for choosing this technology:**
Dimensional modeling approach’s ability to simplify complex data structures makes it easier for business analysts to complete Online Analytical Processing (OLAP) tasks. Scalability and efficient query performance are made possible by this design which is crucial in the rapidly expanding e-commerce sector. Although other technologies aren’t specifically covered in the paper the use of dimensional modeling aligns with industry best practices for e-commerce data warehouse design.
**Important Use case:**
One significant use case that is covered is the analysis of consumer buying trends to inform marketing strategies and inventory management. The e-commerce platform can use the data warehouse to execute complex queries that identify seasonal trends product associations and purchasing patterns. This makes it possible to make data-driven decisions that raise operational efficacy and customer satisfaction. 
**Access Management Considerations:**
Managing access effectively is crucial for internal stakeholders such as marketing teams inventory managers and business analysts to have the proper access to the data needed for their work. In order to ensure data privacy and compliance with legal requirements the data warehouse design must incorporate security features that control access levels. Role-based access controls can be used to provide stakeholders with the information relevant to their roles while protecting sensitive data from unauthorized access. 
This case study demonstrates the importance of a well-designed data warehouse in fulfilling the analytical needs of e-commerce platforms facilitating informed decision-making and maintaining a competitive edge in the online market. (LeVan-Shultz, 2001).


**CONCLUSION**
For this project I successfully designed implemented and used a comprehensive data warehouse that was specifically designed for analyzing key business metrics using MySQL. During the project phases both conceptual and physical ER diagrams were created in order to effectively map out and arrange the database structure. These diagrams ensured data integrity and efficiency by simplifying the process of normalizing the database schema up to the third normal form (3NF). 

I created realistic data sets with the Faker library in Python and used them to fill the database. Information about clients’ vendors orders and associated entities were all included in these data sets. With this configuration a real-world scenario where dynamic data interaction is common was simulated.

Using a number of meticulously constructed SQL queries I linked sales and profitability with product reviews and ratings looked at consumer purchasing patterns and identified the most profitable vendors. These queries not only demonstrated the value of the data warehouses but also provided valuable insights into market trends and consumer behavior. I created a stored procedure for monthly report creation in order to further expedite the collection and assessment of monthly performance data. This automation is a significant step toward improving operational efficiency. 
The projects outcome clearly demonstrates the data warehouse’s ability to enhance decision-making and offer practical business insights. My ability to effectively manage and work with large data sets ensuring that all business needs are met if not exceeded is demonstrated by the completion of this project. This experience demonstrates that I am a proficient data analyst capable of significantly contributing to data-driven projects.
