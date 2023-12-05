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
I'll maybe make an explination later if I'm not busy

[![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api25Braeden=anuraghazra)](https://github.com/anuraghazra/github-readme-stats)
