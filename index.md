# Part 1
## StringServer

### StringServer code:
![Screenshot 2023-01-30 205254](https://user-images.githubusercontent.com/110417453/215668731-230517e5-ffb4-40f9-b45d-6569f3d52996.png)
![Screenshot 2023-01-30 205221](https://user-images.githubusercontent.com/110417453/215668757-47cde082-d29f-4670-a63c-255264f351d2.png)

### Add message: Hello

![Screenshot_20230130_085448](https://user-images.githubusercontent.com/110417453/215669195-a8d8d01f-884b-4257-a1a1-a5f7f9d2bcee.png)

From the URI `/add-message?s=Hello`, the handleRequest method is called from the Handler class. Since it contains `/add-message`, the code will then try to find the parameters. The code runs `url.getQuery().split("=")` which returns everything after the `?` in the URI, and splits it on the `=` sign. Since the first part of the query is correctly identified as `s`, the code then runs the method `addString(parameters[1])`, where `parameter[1]` is `"Hello"`. This concatenates the argument from the query, `"Hello"`, to the running String with a line break `\n` at the end. Initially, the running String is an empty String `""`. After concatenating, the handler then returns the running String, which now is `Hello\n`.

### Add message: 12345dsfs

![Screenshot_20230130_085503](https://user-images.githubusercontent.com/110417453/215669256-4ba4332f-48d5-447b-9d8c-465442292d5b.png)

The second `/add-message` adds `12345dsfs` to the running String. Similar to the first instance above, the handleRequest method is called and since the URI contains `add-message`, the query is found and split into parameters. `Parameter[1]` is `"12345dsfs"`. The `addString(parameters[1])` method is called to add `12345dsfs` to the running String. Before this, the running String was `Hello\n`, but after `addString` is called, the new concatenated running String is `Hello\n12345dsfs\n`. The `\n` indicate new lines, which result in the newest message to be displayed below the first message.

---

# Part 2
## Bug from Lab 3

### ArrayExamples.averageWithoutLowest(double[] arr)

Original Code:

![Screenshot_20230130_101116](https://user-images.githubusercontent.com/110417453/215680771-231e6b48-8298-49d9-9912-13df741380cf.png)

### Passing test

```
    @Test
    public void testAverageWithoutLowestPass() {
        double[] input = {1, 2, 3};
        double average = ArrayExamples.averageWithoutLowest(input);
        assertEquals(2.5, average, 0.001);
    }
```

![Screenshot_20230130_102438](https://user-images.githubusercontent.com/110417453/215682935-8be57896-6407-4d29-bdb8-d298db1db3ef.png)

### Failing test

```
    @Test
    public void testAverageWithoutLowestFail() {
        double[] input1 = {1,1,2,2};
        double average = ArrayExamples.averageWithoutLowest(input1);
        assertEquals(2, average, 0);
    }
```

![Screenshot_20230130_102514](https://user-images.githubusercontent.com/110417453/215683042-cdd30049-b8b5-4f5d-9e38-5446a5f33b3c.png)

### Required change:

Before:
```
    for(double num: arr) {
        if(num != lowest) { sum += num; }
    } 
    return sum / (arr.length - 1);
}
```

After:
```
    for(double num: arr) {
        if(num != lowest) { sum += num; }
        else {removed++;}
    } 
    return sum / (arr.length - removed);
}
```

The main issue with the code was that if there were multiple instances of the lowest number, it would properly not include them in the sum, but when calculating the 
average by dividing the sum by the number of numbers, it would only do `arr.length - 1`, assuming that there was only 1 instance of the lowest number. 

The way to fix this was to create a counter called `removed` which would iterate every time a number wasn't included in the sum. Then, when returning the average, the sum would properly divide by `arr.length - removed` which would give an accurate number of numbers included in the sum.

Final Code:

![Screenshot_20230130_101415](https://user-images.githubusercontent.com/110417453/215681172-b033c04a-0bfb-49c1-a24a-4d7be79c198c.png)

---

# Part 3

