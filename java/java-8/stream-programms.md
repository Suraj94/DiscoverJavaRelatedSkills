### find the second largest value from the list using stream

```
List<Integer> values  = new ArrayList<>();
        values.add(1);
        values.add(2);
        values.add(3);
        values.add(4);
        values.add(5);
        values.add(5);
        Optional<Integer>integer = values.stream().distinct().sorted(Comparator.reverseOrder()).skip(1).findAny();
        System.out.println(integer.get());
```
--------------------------------------------------------------------------------------------------------------------------------
### Frequancy of the each characters in the string

```
String str = "surajss";
        Map<Character, Long> map =
                str.chars().mapToObj(c -> (char)c).collect(Collectors.groupingBy(Function.identity(),
                Collectors.counting()));
        System.out.println(map);
```
#### Function.identity

This is function utility which is basically used always with the `Collectors.groupingBy.` This will be provided the output as the argument which you passed.
In the above example character is returned as the output of this function. 
So in case of groupingBy key will be characters.

#### Collectors.counting

This utility used to count the elements from the stream/collector. In the above example we have used with the groupBy so it will be counting the elements from each group and returned in the map.

--------------------------------------------------------------------------------------------------------------------------------

### frquancy of the each element from the array list

```
List<String> elements  = new ArrayList<>();
        elements.add("suraj");
        elements.add("suraj1");
        elements.add("suraj2");
        elements.add("suraj");

        Map<String, Long> map = elements.stream().collect(Collectors.groupingBy(Function.identity(),
                Collectors.counting()));

        System.out.println(map);
```

This will be resolved by the same approach which is used above.

--------------------------------------------------------------------------------------------------------------------------------
### join the list of string with the delemeter ,prefix and sufix into single string 
```
List<String> elements  = new ArrayList<>();
        elements.add("suraj");
        elements.add("suraj1");
        elements.add("suraj2");
        elements.add("suraj");

        String joiningStr = elements.stream().collect(Collectors.joining("-","pre","suf"));
        System.out.println(joiningStr); \\ presuraj-suraj1-suraj2-surajsuf
```

#### Collectors.joining

This will be used for joining of the strings by applying of the delemeter and prefix and suffix if provided. If nothing has been prvided then it will just concatinate the strings are provide the single string in result.

--------------------------------------------------------------------------------------------------------------------------------

### find the max element from the list 

```
List<Integer> intergers = new ArrayList<>();
        intergers.add(1);
        intergers.add(10);
        intergers.add(100);
        intergers.add(1000);
        Integer streamMax =  intergers.stream().max(Comparator.naturalOrder()).get();
        System.out.println(streamMax);

        Integer integer = intergers.stream().collect(Collectors.maxBy(Comparator.naturalOrder())).get();
        System.out.println(integer);
```

This will be resolved by the two approaches. by using the stream.max function which takes the comparator as arguments and another is the Colelctors.maxBy function.
puspose of this both the functions are same. and accepting the compartor as argument only. 
The stream method is directly applied on the evert element form the collection. were the maxBy function is comes along with the collect method which means that it will be applied after collection of the elements.

#### Comparator.naturalOrder

We have used this order in the max and maxBy function. natural order means that we don;t needs to be implement the compartor interface for the ordering for the types such as String, numbers and dates. they are order natually.
This internally uses the comparable compareTo method to order the data.
If you want to apply the natural order on the custom objects such as the Person then you have to implement the comprable interface and provide the compareTo method implementation.
--------------------------------------------------------------------------------------------------------------------------------

### find the string are anagram of each other or not. which means that if we re arrange the letters then the string should match each other

```
String anagram = "aba";
        String anagram2 = "baa";

        String reverseAnagram =
                anagram.chars().mapToObj(c -> (char)c).sorted().map(ch -> ch.toString()).collect(Collectors.joining());

        String reverseanagram2 =
                anagram2.chars().mapToObj(c -> (char)c).sorted().map(ch -> ch.toString()).collect(Collectors.joining());
        System.out.println(reverseAnagram.equals(reverseanagram2)); \\ true
```

Here we have sorted the string by char and then joined the string by collectors.joining and then compared with each other.

--------------------------------------------------------------------------------------------------------------------------------

### sum the list of the integers 

```
 List<Integer> numbers = new ArrayList<>();
      numbers.add(1);
        numbers.add(2);
        numbers.add(3);

        int sum = 0;
        Integer value = numbers.stream().reduce(sum, (num1 , num2) -> num1 + num2);
        System.out.println(value); \\ 6
```
#### reduce

reduce method is used when you want to accumilate the result. in this function we have to first argument provide the accumilation function which means that were the result will be stored. in this example we have sum varaible which will hold the result on every iteration and will give you the final result. 

Then next will be function which accept two arguments one is prev value and another is next value and you can provide the implementation for this values and then result will be accumilated into the sum.

--------------------------------------------------------------------------------------------------------------------------------

### find the first three min and max values from the list 

```
 List<Integer> numbers = new ArrayList<>();
      numbers.add(1);
        numbers.add(2);
        numbers.add(3);
        numbers.add(4);
        numbers.add(5);
        numbers.add(6);

       List<Integer> minValues =  numbers.stream().sorted().limit(3).collect(Collectors.toList());
        System.out.println(minValues);

       List<Integer> maxValues =
               numbers.stream().sorted(Comparator.reverseOrder()).limit(3).collect(Collectors.toList());

        System.out.println(maxValues);
```

#### limit

We have used limit here which is used to limit the first element from the list to the range which is specified.
which means that first range specified elements will be only available and other are discarded.
--------------------------------------------------------------------------------------------------------------------------------
### find the duplicate elements from the stream

```
ArrayList<String> lists = new ArrayList<>();
        lists.add("a");
        lists.add("b");
        lists.add("c");
        lists.add("c");

        Set<String> set = new HashSet<>();

        List<String> duplicateEle =  lists.stream().filter(item -> !set.add(item)).collect(Collectors.toList());
        System.out.println(duplicateEle);
```
--------------------------------------------------------------------------------------------------------------------------------