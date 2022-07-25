+++
title = "Hangman"
date = "2020-05-17"
[taxonomies]
tags = ["python", "tech"]
+++

Every millenial kid knows the traditional Hangman game. The player has to guess the letters of a secret word. With each wrong guess, a portion of the hanging figure is revealed and if you are not able to guess the letters before the complete figure of the hangman is revealed, the game gets over.

In this project, we are going to create a simple, minimal, terminal based version of the game with the using Python. Like we do for every project, we shall begin with the algorithm and then code it.

## Algorithm

- The computer chooses a word randomly from a list of words stored in a file.
- The user is presented with a greeting and then asked to enter a letter.
- If the letter is present in the word, its position is revealed.
- If the letter is not present in the word, then we reveal a portion of the hanged figure.
- If the all correct letters are not found before revealing the complete figure, the game ends.

## Code

Before we begin, we will need to create the figure of Hangman. Since we are going to be working on the terminal, ASCII art could be really helpful here. We can create 6 or 7 variations of the Hangman figure, each one progressively revealing more of the Hangman than the previous one. The complete `art.py` file can be found in the Github repository for this project. Therefore, I am including only the final figure of the Hangman here:

```

	=========
	|   |   |
	|   |   |
	|   O   |
	| /-+-/ |
	|   |   |
	|  | |  |
	|  | |  |
	|       |
	=========

```

I've created the complete sequece of the above art and in the module `art.py`. Therefore, we will need to import that. Additionally, since we are going to be referring to a list of words stored in an external file, we shall also need the `csv` module and the `random` module to choose a random workd from the file.

```python
from art import hangman_art
import csv
import random
```

Let's steal this function that we have used earlier in the Word Jumble game. This function essentially imports the words form the external file into a list.

```python
def getWords(filename):
elements = []
with open(filename, 'r') as csvfile:
csvreader = csv.reader(csvfile)
for element in csvreader:
elements.append(element)
return elements
```

Next we do some initial setup. We assign our ASCII art figures to the variable `HANGMAN`. The maximum tries allowed is 1 less than the length of the word because we start with the ASCII figure of the empty hanging pit. The variable `wrong` keeps track of the number of wrong attempts made and the variable `guess_so_far` shows the letters that are correctly guessed in the respective positions of the word. The list `used` collects all the letters that have been entered already in order to prevent duplication.

```python
HANGMAN = hangman*art()
max_tries = len(HANGMAN) - 1
word = random.choice(getWords('words.csv'))[0]
wrong = 0
guess_so_far = "_"*len(word)
used = []
```

Let's add some greetings to make the game more welcoming.

```python
print("HANGMAN")
print("=======")
print('''
    Welcome to Hangman game.
    Guess the all the letters or get hanged!
''')
```

Next we enter the main part of the code, the `while` loop. The loop
sustains as long as the number of tries does not exceed the leghth of
the word or the word is guessed. The loop consists of 3 sections:

- Print the current status and prompt for new guess
- Check the guessed letter is a duplicate
- Check if the guess is in the word

```python
while(wrong < max_tries and guess_so_far != word):

    # Print status
    print(HANGMAN[wrong])
    print("You've used the following letters:\t {}.".format(used))
    print("The word so far is {}.".format(guess_so_far))
    guess = input("Enter a letter:\t")

    # Check if letter is already guessed
    while guess in used:
        guess = input('''
            You've already guessed this.
            Guess another letter:\t''')

    # Append newly guessed letter to used
    used.append(guess)

    # Check guess
    if guess in word:
        print("Yes! {} is in the word!".format(guess))
        blanks = ""
        for i in range(len(word)):
            if(guess == word[i]):
                blanks += guess
            else:
                blanks += guess_so_far[i]
        guess_so_far = blanks
    else:
        print("Sorry! {} isn't in the word.".format(guess))
        wrong += 1

```

The first section, as the comment suggests, it simply displays the
status and prompts the user to enter a new guess. When a letter is
entered, the program checks if the letter was previously entered by
checking the `used` list. If the letter is being entered for the first
time, it is appended to `used` list.

Next, if the guessed letter is present in the word, then the
`guess_so_far` string is updated to reveal the position(s) of the
guessed letter while the remain letters of the word are replaced by
blanks.

Finally, to the end the game, if the number of wrong attempts has
exceeded the length of the word, then we display the complete picutre
of the hangman other wise we congratulate the player.

```python
if(wrong == max_tries):
print(HANGMAN[wrong])
print("You have been hanged! GAME OVER!")
else:
print("Congratulations! You guessed it!")
print("The word was {}.".format(word))
```

The complete code can be found on my Github page [here](https://github.com/s4m13337/hangman).
