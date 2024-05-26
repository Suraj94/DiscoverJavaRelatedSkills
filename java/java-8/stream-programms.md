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
