# escape_from_markov

CTF: iCTF 2023

Date: December 3rd, 2023

Category: data science

Points: 498

## Description:

We made a fake flag generator just for this CTF! It can generate flags that look like the real one! Can you find the real flag?

`nc 0.cloud.chals.io 34879`

## Solution:

We are given the source code for the server. Inspecting the code, we see that the program generates some strings of text, 20% of which is the real flag, as the input data. It inputs this into a Markov chain algorithm that finds the probabilities of the following characters given each preceding character. It then uses these probabilities to build possible output strings and prints these to the screen.

This means that, looking at the output data, for each character in the true flag, 20% of the time, that character will be followed by the next character in the true flag. We could write a script to scan the output data, construct the probabilities, and see which ones match the 20%, but it turns out it is easier to just inspect the data manually and construct the flag. It helps to notice that there are capital letters in the output data which aren't from the random input data, so you know that those capital letters and the following characters are definitely in the string.

The flag is `ictf{mark0v1an_N1gh7maR3s}`.
