# Advent Of Code 2023
> [!Important]<br>
> By viewing and/or using any of my work you agree to the [license](https://choosealicense.com/licenses/mpl-2.0/)

This is a directory where I will be storing all my submissions for the Advent of Code 2023. This will be updated as I do more of the problems. Everything here will be done in Java (Maybe a tiny bit of python if I'm bored) and I probably won't complete all 24. Anyways without further ado,

## Table of contents
  - [Problem 1](https://github.com/25Braeden/AdventOfCode2023/blob/main/README.md#problem-1)
    - [Solution](https://github.com/25Braeden/AdventOfCode2023/blob/main/README.md#solution)

## Problem 1
> If you just want to duplicate my code, you can [here](https://github.com/25Braeden/AOC-Day-1)
### Solution
**You will need to make some minor changes before running the code**
Here is the changes you need to make:
  1. Change `class` from `public class Day1 {` to `public class (Enter your file name without the ".java") {`
  2. Make a file called `(anything you want).txt` and paste the provided strings that they give you
  3. Change `String filePath = "/workspaces/codespaces-blank/puzzle.txt";` to `String filePath = "(Path to file we just made).txt";`
Now that that's done, you should be able to run the code.<br>
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Day1 {
    public static void main(String[] args) {
        try {
            String filePath = "/workspaces/codespaces-blank/puzzle.txt";
            int sum = calculateCalibrationSum(filePath);
            System.out.println("Sum of calibration values: " + sum);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static int calculateCalibrationSum(String filePath) throws IOException {
        int sum = 0;

        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                int firstDigit = findFirstNumber(line);
                int lastDigit = findLastNumber(line);

                if (firstDigit != -1 && lastDigit != -1) {
                    int calibrationValue = firstDigit * 10 + lastDigit;
                    sum += calibrationValue;
                }
            }
        }

        return sum;
    }

    private static int findFirstNumber(String s) {
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                return Character.getNumericValue(c);
            }
        }
        return -1;
    }

    private static int findLastNumber(String s) {
        for (int i = s.length() - 1; i >= 0; i--) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                return Character.getNumericValue(c);
            }
        }
        return -1;
    }
}
```
### Breakdown
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
```
These are the import libraries that we will need for this project. BufferedReader in combination with FileReader can be used to read/parse .txt files<br>
<br>
> [!Note]<br>
> I will not be explaining top -> bottom as I think it will be easier explaining certain sections first<br>

#### Finding the numbers
```java
private static int findFirstNumber(String s) {
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                return Character.getNumericValue(c);
            }
        }
        return -1;
    }
```
Let's break this down,<br>
`private static int findFirstNumber(String s) {`<br>
Here we make a method called `findFirstNumber`. This will take a String as an input and will refrence the String as "s".<br>
This is similar to how we use "i" when doing a for loop.<br>
We can then iterate through the string that we just passed into `findFirstNumber` by using `for (char c : s.toCharArray())`<br>
The program then checks if the character in the string is a intiger by using `if (Character.isDigit(c)){`<br>
Finally we return the value of the intiger using `return Character.getNumericValue(c);`<br>
`return -1` is used incase there is no digit in the code<br>

Now to get the last number<br>
```java
private static int findLastNumber(String s) {
        for (int i = s.length() - 1; i >= 0; i--) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                return Character.getNumericValue(c);
            }
        }
        return -1;
    }
```
We again start by making a method `findLastNumber`<br>
Lets look at this for loop,
  - `for (int i = s.length() -1;`
    > This makes "i" the length of the string, meaning it will start at the end of the string instead of the beginning
  - `i >= 0; i--`
    > "i" will go from the last character in the string up until the first
  - `char c = s.charAt(i)`
    > We make a new variable that is a character called "c". "c" is the character at i

  - ```java
    if (Character.isDigit(c)) {
                return Character.getNumericValue(c);
            }
    ```
    > If character "c" is a digit/intiger, it gets returned.
  - `return -1;`
    > If there is no intiger we return a value of -1

#### Calculation
##### Now that we have the numbers we need to add them to a rolling total, heres how we do this
```java
private static int calculateCalibrationSum(String filePath) throws IOException {
        int sum = 0;

        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                int firstDigit = findFirstNumber(line);
                int lastDigit = findLastNumber(line);

                if (firstDigit != -1 && lastDigit != -1) {
                    int calibrationValue = firstDigit * 10 + lastDigit;
                    sum += calibrationValue;
                }
            }
        }

        return sum;
    }
```
Lets break this down piece by piece again:
  - `private static int calculateCalibrationSum(String filePath) throws IOException {`
    + we make a new method called `calculateCalibrationSum` that will return an intiger<br>
    + we pass a `String` variable called `filePath`(Don't worry we will get to filePath in the next part) into the method<br>
    + `throws IOException` **Please ignore this for now** basically, its just a way of circumventing a potential error, just know that you need it<br>
  - `int sum = 0;`, we start the sum variable where we will add numbers to it
  - `try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {`, lets look at this
    + We use `try` in case there is a problem when attempting to open the file, ignore this for now<br>
    + `BufferedReader reader = new BufferedReader(new FileReader(filepath))) {`. This might look complicated, but it really isn't. Remember when using a scanner we have to enter,
      `Scanner scanner = new Scanner(System.in)`? This is just that. We make a variable called `reader` which will represent our BufferedReader. BufferedReader will allow us to read
      text from the file containing all of our puzzle pieces. We add `new FileReader` as its common to use FileReader with BufferedReader, as FileReader can read text one line at a time
      and BufferedReader is used when you have large batches of text, like what we have.
    + `FileReader(filepath)`, we just specify that FileReader will be opening the variable `filepath`
  - `String line;` This is a String variable that will represent one of the 1000 lines in our text document
  - `while ((line = reader.readLine()) != null) {` All this does is take one line from your txt document and it reads it until it ends (until its null)
  - ```java
    int firstDigit = findFirstNumber(line);
    int lastDigit = findLastNumber(line);
    ```
    Here we call the methods we made earlier to gather the first and last digits
  - `if (firstDigit != -1 && lastDigit != -1) {` Remember how we made it so that if there wasn't a first or last digit it returned -1? Well this line checks and makes sure that neither of
    the values are -1, essentially it makes sure that there is a first and last digit
  - `int calibrationValue = firstDigit * 10 + lastDigit;` We make a new int `calibrationValue` that is the first and last digit. The reason we do times 10, is because the website
    wanted it to be that if you were given "hj3fhgf7" it would return "37", so we need to multiply the first digit by 10 before adding
  - `sum += calibrationValue`, we add the value we just got to the rolling sum, allowing us to have a total of all the numbers
  - `return sum`, this returns the value of sum so we can use it in other parts of the code

#### Locating txt document and printing sum
All the hard stuff is done! All thats left now are these couple lines<br>
```java
public static void main(String[] args) {
        try {
            String filePath = "/workspaces/codespaces-blank/puzzle.txt";
            int sum = calculateCalibrationSum(filePath);
            System.out.println("Sum of calibration values: " + sum);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
Break it down one last time:
  - `String filePath = "/workspaces/codespaces-blank/puzzle.txt";` this is the `filepath` variable I've been refrencing this whole time. All you need to do is tell netbeans (or whatever
    IDE your using) where the file containing all your puzzles are located so it can access it. You will need to change this for your own project to math your path.
  - `int sum = calculateCalibrationSum(filepath);` we make an int called `sum` that uses the method we just made to extract and add all the first and last intigers to it
  - `System.out.println("Sum of calibration values: " + sum);`, finally you can see what the sum is
  - ```java
    catch (IOException e) {
            e.printStackTrace();
        }
    ```
    Once again ignore this, this is here to stop the program from breaking if there is a problem with your file. We need it because we used try{<br>

### And done!
Congrats! Looks like we've completed the first advent! Please follow me.
