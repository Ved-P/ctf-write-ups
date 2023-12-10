# Mystical Castle

CTF: iCTF 2023

Date: December 4th, 2023

Category: misc

Points: 499

## Description:

The description is a long story about finding one's way to a mystical castle. There are rooms we need to move through, and each room needs two keys to open. Most of the description is not relevant, except for the final paragraphs:

Find a way to reach The Forbidden Throne Room using two parts of the book discovered in the Whispering Gallery, namely `castle_domain.pddl` and `castle_problem_poem.pddl`.

Once you found a plan to escape the castle, your flag content is the first two letters of each room visited in order.

## Solution:

`.pddl` is the extension for a programming language used to plan the actions of an AI agent. The domain file explains what the possible states of the program can be as well as the actions the AI can take to modify the state of the program. For this problem specifically, this means moving from room to room and picking up keys. Nothing needs to be changed here.

The problem file details the starting and ending conditions for the specific scenario we want to run. This enables the AI to figure out what actions it can take to convert the start condition to the end condition. However, this problem file contains poetry that we need to change to `.pddl` expressions so that the code can compile.

For example, the starting condition was initially described as this:

```
;at
In Whispering Gallery begins our tale,
```

We can change this to:

```
(at whispering_gallery)
```

As another example, we can look at what rooms are opened with which keys:

```
;opens_with
Atop a vault of shadows, silent, steep, topaz, pearl keys awake its sleep.
Crypt sunken 'neath the time's decree, opal, garnet turn the key.
Cell of frostbound, age-old hex, yields to pearl and onyx's behest.
```

These can be changed to:

```
(opens_with shadowy_vault topaz_key pearl_key)
(opens_with sunken_crypt opal_key garnet_key)
(opens_with frozen_cell pearl_key onyx_key)
```

Using a similar process, we convert the rest of the file to `.pddl` syntax. After this is done, we can run these files by downloading the `pddl` extension for VS Code and then executing the files in VS Code. This will pop up a window showing all the actions taken by the AI. We can look through each of the move actions and concatenate the first two characters of the names of each room to find the key: `ictf{whenmiwimoshsufrphsekncrmystsiecfo}`.

Note: this problem can also be solved by hand, but when constructing the flag, you should only include the rooms where keys were picked up, not intermediate rooms that were passed through to reach other rooms.
