# hangman-game
import random

# ASCII art for the hangman
HANGMAN_PICS = [
    """
     -----
     |    |
          |
          |
          |
          |
    =========
    """,
    """
     -----
     |    |
     O    |
          |
          |
          |
    =========
    """,
    """
     -----
     |    |
     O    |
     |    |
          |
          |
    =========
    """,
    """
     -----
     |    |
     O    |
    /|    |
          |
          |
    =========
    """,
    """
     -----
     |    |
     O    |
    /|\\   |
          |
          |
    =========
    """,
    """
     -----
     |    |
     O    |
    /|\\   |
    /     |
          |
    =========
    """,
    """
     -----
     |    |
     O    |
    /|\\   |
    / \\   |
          |
    =========
    """
]

# Word categories
WORD_CATEGORIES = {
    "Animals": ["elephant", "giraffe", "kangaroo", "tiger", "zebra"],
    "Countries": ["brazil", "canada", "japan", "india", "germany"],
    "Movies": ["katera", "Raate", "Kranthi", "Rocky", "Ram"]
}

# Difficulty levels
DIFFICULTY_LEVELS = {
    "Easy": 8,
    "Medium": 6,
    "Hard": 4
}

def get_word(category):
    return random.choice(WORD_CATEGORIES[category]).lower()

def display_hangman(tries):
    return HANGMAN_PICS[tries]

def hangman():
    print("Welcome to Hangman!")
    
    # Choose a category
    print("\nChoose a category:")
    for i, category in enumerate(WORD_CATEGORIES.keys(), 1):
        print(f"{i}. {category}")
    category_choice = int(input("Enter the number of your choice: "))
    category = list(WORD_CATEGORIES.keys())[category_choice - 1]

    # Choose a difficulty level
    print("\nChoose a difficulty level:")
    for i, level in enumerate(DIFFICULTY_LEVELS.keys(), 1):
        print(f"{i}. {level}")
    difficulty_choice = int(input("Enter the number of your choice: "))
    difficulty = list(DIFFICULTY_LEVELS.keys())[difficulty_choice - 1]
    max_tries = DIFFICULTY_LEVELS[difficulty]

    # Get a random word
    word = get_word(category)
    word_completion = "_" * len(word)
    guessed = False
    guessed_letters = []
    guessed_words = []
    tries = 0
    
    print("\nLet's start the game!")
    print(display_hangman(tries))
    print(word_completion)

    while not guessed and tries < max_tries:
        guess = input("\nGuess a letter or the whole word: ").lower()

        if len(guess) == 1 and guess.isalpha():
            if guess in guessed_letters:
                print("You already guessed that letter.")
            elif guess not in word:
                print(f"{guess} is not in the word.")
                tries += 1
                guessed_letters.append(guess)
            else:
                print(f"Good job! {guess} is in the word.")
                guessed_letters.append(guess)
                word_completion = "".join(
                    [guess if word[i] == guess else word_completion[i] for i in range(len(word))]
                )
                if "_" not in word_completion:
                    guessed = True

        elif len(guess) == len(word) and guess.isalpha():
            if guess in guessed_words:
                print("You already guessed that word.")
            elif guess != word:
                print(f"{guess} is not the word.")
                tries += 1
                guessed_words.append(guess)
            else:
                guessed = True
                word_completion = word
        else:
            print("Invalid guess. Please enter a single letter or the full word.")

        print(display_hangman(tries))
        print(word_completion)

    if guessed:
        print("\nCongratulations! You guessed the word!")
    else:
        print(f"\nYou lost! The word was '{word}'.")
hangman()
out put:
Welcome to Hangman!

Choose a category:
1. Animals
2. Countries
3. Movies
Enter the number of your choice: 3

Choose a difficulty level:
1. Easy
2. Medium
3. Hard
Enter the number of your choice: 2

Let's start the game!

     -----
     |    |
          |
          |
          |
          |
    =========

_______

Guess a letter or the whole word: k
Good job! k is in the word.

     -----
     |    |
          |
          |
          |
          |
    =========

k______

Guess a letter or the whole word: p
p is not in the word.

     -----
     |    |
     O    |
          |
          |
          |
    =========

k______

Guess a letter or the whole word: r
Good job! r is in the word.

     -----
     |    |
     O    |
          |
          |
          |
    =========

kr_____

Guess a letter or the whole word: u
u is not in the word.

     -----
     |    |
     O    |
     |    |
          |
          |
    =========

kr_____

Guess a letter or the whole word: a
Good job! a is in the word.

     -----
     |    |
     O    |
     |    |
          |
          |
    =========

kra____

Guess a letter or the whole word: n
Good job! n is in the word.

     -----
     |    |
     O    |
     |    |
          |
          |
    =========

kran___

Guess a letter or the whole word: t
Good job! t is in the word.

     -----
     |    |
     O    |
     |    |
          |
          |
    =========

krant__

Guess a letter or the whole word: h
Good job! h is in the word.

     -----
     |    |
     O    |
     |    |
          |
          |
    =========

kranth_

Guess a letter or the whole word: i
Good job! i is in the word.

     -----
     |    |
     O    |
     |    |
          |
          |
    =========

kranthi

Congratulations! You guessed the word!
PS C:\Users\rr175\OneDrive\Desktop\pyscript\pyscript> 
