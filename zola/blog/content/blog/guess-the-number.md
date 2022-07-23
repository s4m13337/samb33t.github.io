+++
title = "Guess the number"
date = "2020-04-12"
[taxonomies]
tags = ["python", "tech"]
+++

This is a classic terminal based game where the computer thinks of a number and the user has to guess it in as minimum number of tries as possible. Although this game is very simple, it teaches us some absolute fundamentals of programming. Let us see how we can develop this from the pseudocode to the finished product.

## Algorithm

- The computer picks a number between 1 and 100 and stores it in memory
- The player guesses the number
- If the guess is correct, show a congratulating message otherwise guess again

Well that seems very plain and simple. Let's add in some more details like showing hints and number of attempts made.

- While the player is guessing
  - If the guessed number is lower than the actual number, tell to guess a larger number
  - If the guessed number is greater than the actual number, tell to guess a smaller number
  - For each guess, increment the tries by 1
- When guess is correct, display the congratulating message along with the number of tries

There we have it. Now we just need to code this into a python file.

## Code

Never forget the Shebang!

```
#!/usr/bin/env python
```

This prgram is going to be guessing numbers between 1 to 100. Therefore we need to import the random module.

```
import random
```

Let's initialize some variables.

```python
number = random.randint(1, 100)
tries = 1
```

Now it's time to hard-code some introductory messages.

```python
print("Welcome to Guess the Number")
print("===========================")
print('''
    I've thought of a number between 1 to 100.
    Try to guess it in as few tries as possible.'''
)
```

And now, here is the core of the program.

```python
guess = int(input("Your guess:\t"))
while(guess != number):
if(guess < number):
guess = int(input("Try guessing a higher number:\t"))
else:
guess = int(input("Try guessing a lower number:\t"))
tries += 1
```

And finally, when everything is done, we wrap up.

```python
print('''
    Congratulations! You guessed the number in {} tries.
    The number is {}'''.format(tries, number)
)
```

The complete code can be found on my Github page [here](https://github.com/s4m13337/guess-the-number).
