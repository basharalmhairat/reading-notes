# Room 

## Defining data using Room entities :

When you use the Room persistence library to store your app's data, you define entities to represent the objects that you want to store. Each entity corresponds to a table in the associated Room database, and each instance of an entity represents a row of data in the corresponding table.

That means you can use Room entities to define your database schema without writing any SQL code
Anatomy of an entity
You define each Room entity as a class that is annotated with @Entity. A Room entity includes fields for each column in the corresponding table in the database, including one or more columns that comprise the primary key.

The following code is an example of a simple entity that defines a User table with columns for ID, first name, and last name:
```
@Entity
public class User {
    @PrimaryKey
    public int id;

    public String firstName;
    public String lastName;
}
```

By default, Room uses the class name as the database table name. If you want the table to have a different name, set the tableName property of the @Entity annotation.
Similarly, Room uses the field names as column names in the database by default. If you want a column to have a different name, add the @ColumnInfo annotation to the
field and set the name property. The following example demonstrates custom names for tables and columns:

```
@Entity(tableName = "users")
public class User {
    @PrimaryKey
    public int id;

    @ColumnInfo(name = "first_name")
    public String firstName;

    @ColumnInfo(name = "last_name")
    public String lastName;
}
```

## Entity:

Marks a class as an entity. This class will have a mapping SQLite table in the database.

Each entity must have at least 1 field annotated with PrimaryKey. You can also use primaryKeys attribute to define the primary key.

Each entity must either have a no-arg constructor or a constructor whose parameters match fields (based on type and name). Constructor does not have to receive all fields as parameters but if a field is not passed into the constructor, it should either be public or have a public setter. If a matching constructor is available, Room will always use it. If you don't want it to use a constructor, you can annotate it with Ignore.

When a class is marked as an Entity, all of its fields are persisted. If you would like to exclude some of its fields, you can mark them with Ignore.

If a field is transient, it is automatically ignored unless it is annotated with ColumnInfo, Embedded or Relation.

Example:

```
@Entity
data class Song (
    @PrimaryKey
    val id: Long,
    val name: String,
    @ColumnInfo(name = "release_year")
    val releaseYear: Int
)
```

## Related entities in Room

An important part of designing a relational database is splitting the data into related tables and pulling the data together in meaningful ways.
Starting with Room 2.2 (now stable) we have support for all possible relations between tables: one-to-one, one-to-many and many-to-many, with one annotation:
@Relation.
![image](https://user-images.githubusercontent.com/97823170/167389153-efefde9c-6f20-4c0f-a3cb-990fdfd15c29.png)
One-to-one relations
Let’s say that we live in a (sad) world where a person can own only one dog and a dog can have only one owner. This is a one-to-one relation. To model this in a relational database, we create two tables: Dog and Owner, where the Dog table has a reference to the owner id, or the Owner has a reference to a dog id. In Room, we create two entities:

```
@Entity
data class Dog(
    @PrimaryKey val dogId: Long,
    val dogOwnerId: Long,
    val name: String,
    val cuteness: Int,
    val barkVolume: Int,
    val breed: String
)
```
```
@Entity
data class Owner(@PrimaryKey val ownerId: Long, val name: String)
```
Let’s say that we want to display the list of all dogs and their owners on the screen. To do this, we would create a DogAndOwner data class:

```
data class DogAndOwner(
    val owner: Owner,
    val dog: Dog
)
```
To query this using SQLite, we would need to 1) run two queries: one that gets all owners, and one that gets all dogs based on owner ids and then 2) handle the object
mapping.

## Accessing data with Room 
For those of you who do not know what is Android Jetpack then

Android Jetpack is a collection of Android software components to make it easier for you to develop great Android apps.
They will help you to

Follow best practices
Free you from writing boilerplate code.
Simplify complex tasks, so you can focus on the code you care about.

Room provides an abstraction layer over SQLite to allow fluent database access while harnessing the full power of SQLite.

Room is now considered as a better approach for data persistence than SQLiteDatabase. It makes it easier to work with SQLiteDatabase objects in your app, decreasing the amount of boilerplate code and verifying SQL queries at compile time.

Why use Room?
Compile-time verification of SQL queries. each @Query and @Entity is checked at the compile time, that preserves your app from crash issues at runtime and not only it checks the only syntax, but also missing tables.
Boilerplate code
Easily integrated with other Architecture components (like LiveData)
Major problems with SQLite usage are

![image](https://user-images.githubusercontent.com/97823170/167389916-ee730b2a-c7cc-4aa7-a75c-bdfaed73484c.png)

There is no compile-time verification of raw SQL queries. For example, if you write a SQL query with a wrong column name that does not exist in real database then it will give exception during run time and you can not capture this issue during compile time.
As your schema changes, you need to update the affected SQL queries manually. This process can be time-consuming and error-prone.
You need to use lots of boilerplate code to convert between SQL queries and Java data objects (POJO).
