### what is changes in the map in the java 8 version of the java ?

There are some performance changes in the hashmap is done in java 8.

As we know that the hashmap is uses the array and linked list data structure to store the element.
![img.png](../screens/img.png)
So, when element is adding into the map ot calculates the hash by hashcode and identify the bucket from the array and store the data in linked list manner.

As there will be chances of having the same hashcode for the one value so that all values will be store in linked list manner.
This can be occurred due to the incorrect hascode implementation which is not evenly distribute the values in the map buckets. And which reduces the retriving time for the values from o(1) to o(n).
![img.png](../screens/map-2.png)

This performance has been improved in java 8. Once the linked list of the bucket is reaches to the threshold value then the values from the bucket will be stored in the tree manner.
which will be reducing time for this from o(n) to the o(log(n))
![img.png](map-3.png)

###  What is the return type of the put method from map

put method is returning the exsting value from the map if alereadt exist. Otherwise it will be return the null value.

```
Map<String,String> map = new HashMap<>();
String value  = map.put("any" , "value");
System.out.println(value) // null

value  = map.put("any" , "value2");
System.out.println(value) // value  --> old value
```

### What is the difference between the perm gen memory and metaspace memory 

Earlier of java 8 is using the perm gen memory to store the meta information of the application such as the class definition , method and field information.

In the java 8 perm gen memory is get replaced with the metaspace memory. were the perm gen memory earlier was an part of the heap memory, and it is an constant size of the memory. Also, earlier there was an not an concept of the loading the classes at the runtime. so when the initially classes are loaded this meta information keeps in the perm gen memort unitl the jvm shutdowns. and now days we can load and unload the classes dynamically due to this there are the chances to get the outOfMemoryError.

This limitation is resolved in the metaspace memory. the task/ask for this memory is the same as the perm gen to store the app meta information. 
But now metaspace is not part of the heam it is an native memory which is comuptated in the OS memory. Also this memory can be increased dynamically so the problem of having the OutOfMemory will be reduced here.

Also, same the perm gen GC will be execued on the metaspace memory as well once it will be reaches to the specific threshold.

