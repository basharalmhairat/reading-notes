# Hash Tables

 A Hash Table is a data structure that stores data in an associative manner. It is made up of two parts: an array, where the data is stored,
 and a Hash Function which is a mapping function. Basically, a Hash Function is a function that takes things from one space and maps them to a space for indexing.
 
 A Hash Table is used to implement structures such as dictionary, map, or associative array and it is a data structure in which insertion and search operations
 are very fast.

The idea behind a Hash Table is that for each element we want to store, we calculate a unique address and we put the value at this index in the array.
When we need to find a value, we once again calculate its index and then return the value. In other words, a Hash Table allows us to store and retrieve objects by key.

![image](https://user-images.githubusercontent.com/97823170/167614749-afc15c58-87f8-4cdc-b64d-157babd79bd2.png)

## what is a hash table?

![image](https://user-images.githubusercontent.com/97823170/167614909-6458fabf-e42a-43a8-b27c-6f34bcb90fb8.png)

Basic Operations
Following are the basic primary operations of a hash table.

Search − Searches an element in a hash table.

Insert − inserts an element in a hash table.

delete − Deletes an element from a hash table.

DataItem
Define a data item having some data and key, based on which the search is to be conducted in a hash table.
```
struct DataItem {
   int data;
   int key;
};
```
Hash Method
Define a hashing method to compute the hash code of the key of the data item.
```
int hashCode(int key){
   return key % SIZE;
}
```
### Search Operation

Whenever an element is to be searched, compute the hash code of the key passed and locate the element using that hash code as index in the array. Use linear probing to get the element ahead if the element is not found at the computed hash code.

Example
```
struct DataItem *search(int key) {
   //get the hash
   int hashIndex = hashCode(key);
	
   //move in array until an empty
   while(hashArray[hashIndex] != NULL) {
	
      if(hashArray[hashIndex]->key == key)
         return hashArray[hashIndex];
			
      //go to next cell
      ++hashIndex;
		
      //wrap around the table
      hashIndex %= SIZE;
   }

   return NULL;        
}
```
### Insert Operation

Whenever an element is to be inserted, compute the hash code of the key passed and locate the index using that hash code as an index in the array. Use linear probing for empty location, if an element is found at the computed hash code.

Example
```
void insert(int key,int data) {
   struct DataItem *item = (struct DataItem*) malloc(sizeof(struct DataItem));
   item->data = data;  
   item->key = key;     

   //get the hash 
   int hashIndex = hashCode(key);

   //move in array until an empty or deleted cell
   while(hashArray[hashIndex] != NULL && hashArray[hashIndex]->key != -1) {
      //go to next cell
      ++hashIndex;
		
      //wrap around the table
      hashIndex %= SIZE;
   }
	
   hashArray[hashIndex] = item;        
}
```
### Delete Operation

Whenever an element is to be deleted, compute the hash code of the key passed and locate the index using that hash code as an index in the array. Use linear probing to get the element ahead if an element is not found at the computed hash code. When found, store a dummy item there to keep the performance of the hash table intact.

Example
```
struct DataItem* delete(struct DataItem* item) {
   int key = item->key;

   //get the hash 
   int hashIndex = hashCode(key);

   //move in array until an empty 
   while(hashArray[hashIndex] !=NULL) {
	
      if(hashArray[hashIndex]->key == key) {
         struct DataItem* temp = hashArray[hashIndex]; 
			
         //assign a dummy item at deleted position
         hashArray[hashIndex] = dummyItem; 
         return temp;
      } 
		
      //go to next cell
      ++hashIndex;
		
      //wrap around the table
      hashIndex %= SIZE;
   }  
	
   return NULL;        
}
```
## basics of hash tables
Hashing is implemented in two steps:

An element is converted into an integer by using a hash function. This element can be used as an index to store the original element, which falls into the hash table.
The element is stored in the hash table where it can be quickly retrieved using hashed key.

hash = hashfunc(key)
index = hash % array_size

In this method, the hash is independent of the array size and it is then reduced to an index (a number between 0 and array_size − 1) 
by using the modulo operator (%).

![image](https://user-images.githubusercontent.com/97823170/167615504-81848e90-f33f-4371-9612-b623304cc9d8.png)

### Hash function

A hash function is any function that can be used to map a data set of an arbitrary size to a data set of a fixed size,
which falls into the hash table. The values returned by a hash function are called hash values, hash codes, hash sums, or simply hashes.

To achieve a good hashing mechanism, It is important to have a good hash function with the following basic requirements:

Easy to compute: It should be easy to compute and must not become an algorithm in itself.

Uniform distribution: It should provide a uniform distribution across the hash table and should not result in clustering.

Less collisions: Collisions occur when pairs of elements are mapped to the same hash value. These should be avoided.

Note: Irrespective of how good a hash function is, collisions are bound to occur. Therefore, to maintain the performance of a hash table,
it is important to manage collisions through various collision resolution techniques.

