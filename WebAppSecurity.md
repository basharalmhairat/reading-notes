## Many to many relationships

Many-to-many relationships are the most commonly used table relationships. They provide crucial information, such as which customers your salespeople have contacted and which products are in customer orders.

A many-to-many relationship exists when one or more items in one table can have a relationship to one or more items in another table. For example:
![image](https://user-images.githubusercontent.com/97823170/161451285-0cfb505f-a393-4cf0-8a85-a2abb8501f32.png)

- Your Order table contains orders placed by multiple customers (who are listed in the Customers table), and a customer may place more than one order.

- Your Products table contains the individual products you sell, which are part of many orders in the Order table.

- One order may include one instance (or more than one instance) of a specific product and/or one instance (or more than one instance) of multiple products.

You create many-to-many relationships differently than you do one-to-one or one-to-many. For those relationships, you simply connect the appropriate fields with a line. To create many-to-many relationships, you need to create a new table to connect the other two. This new table is called an intermediate table (or sometimes a linking or junction table).

In the scenario described earlier, you create an Order Details table with records that contain, for each item in any given order, the ID from the Order table and the ID from the Products table. You create a primary key for that table using the combined keys from the two tables.

In our scenario, Elizabeth Andersen’s order number 1012 consists of products 12, 15, and 30.

Create fields in the intermediate table
As the first table column, Access automatically adds an ID field. Change that field to match the ID of the first table in your many-to-many relationship. For example, if the first table is an Orders table called Order ID, and its primary key is a number, change the name of the ID field in the new table to Order ID and, for the data type, use Number.

![image](https://user-images.githubusercontent.com/97823170/161451275-714edc0f-9083-4b9d-9858-ec80bb7c3951.png)

In Datasheet View, select the ID column heading and then type the new name for the field.

Select the field you just renamed.

On the Fields tab, under Data type, select a data type to match the field in the original table, such as Number or Short Text.

Select Click to Add, and then select a data type that matches the primary key in the second table. In the column heading, which is already selected, type the name of the primary key field from the second table, such as Product ID.
![image](https://user-images.githubusercontent.com/97823170/161451302-03de1698-ded2-4b72-a05b-f01066ba7d78.png)

If you need to track any other information about these records, such as item quantity, create additional fields.


## Security: a humorous overview
![image](https://user-images.githubusercontent.com/97823170/161451525-93cafa0c-1ea2-47ed-8db9-fe2a5a80ac57.png)

The modern software developer has to be something of a swiss army knife. Of course, you need to write code that fulfills customer functional requirements. It needs to be fast. Further you are expected to write this code to be comprehensible and extensible: sufficiently flexible to allow for the evolutionary nature of IT demands, but stable and reliable. You need to be able to lay out a useable interface, optimize a database, and often set up and maintain a delivery pipeline. You need to be able to get these things done by yesterday.
Somewhere, way down at the bottom of the list of requirements, behind, fast, cheap, and flexible is “secure”. That is, until something goes wrong, until the system you build is compromised, then suddenly security is, and always was, the most important thing.


Security is a cross-functional concern a bit like Performance. And a bit unlike Performance. Like Performance, our business owners often know they need Security, but aren’t always sure how to quantify it. Unlike Performance, they often don’t know “secure enough” when they see it.

So how can a developer work in a world of vague security requirements and unknown threats? Advocating for defining those requirements and identifying those threats is a worthy exercise, but one that takes time and therefore money. Much of the time developers will operate in absence of specific security requirements and while their organization grapples with finding ways to introduce security concerns into the requirements intake processes, they will still build systems and write code.

Encode HTML Output
In addition to limiting data coming into an application, web application developers need to pay close attention to the data as it comes out. A modern web application usually has basic HTML markup for document structure, CSS for document style, JavaScript for application logic, and user-generated content which can be any of these things. It's all text. And it's often all rendered to the same document.
![image](https://user-images.githubusercontent.com/97823170/161451519-f421c7bd-16a5-4602-a507-394e9ff9f8e8.png)
An HTML document is really a collection of nested execution contexts separated by tags, like <script> or <style>. The developer is always one errant angle bracket away from running in a very different execution context than they intend. This is further complicated when you have additional context-specific content embedded within an execution context. For example, both HTML and JavaScript can contain a URL, each with rules all their own.

Output Risks
HTML is a very, very permissive format. Browsers try their best to render the content, even if it is malformed. That may seem beneficial to the developer since a bad bracket doesn't just explode in an error, however, the rendering of badly formed markup is a major source of vulnerabilities. Attackers have the luxury of injecting content into your pages to break through execution contexts, without even having to worry about whether the page is valid.

Handling output correctly isn't strictly a security concern. Applications rendering data from sources like databases and upstream services need to ensure that the content doesn't break the application, but risk becomes particularly high when rendering content from an untrusted source. As mentioned in the prior section, developers should be rejecting input that falls outside the bounds of the contract, but what do we do when we need to accept input containing characters that has the potential to change our code, like a single quote ("'") or open bracket ("<")? This is where output encoding comes in.
  
  
