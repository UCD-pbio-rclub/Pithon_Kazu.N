
# 1. Hangman: Copy or write the hangman game and then fix the problems in the game which are listed on pg. 55



```python
# 4_4_hagman_words
import random
words=['chicken','dog','cat','mouse','frog']
def pick_a_word():
    return random.choice(words)

print(pick_a_word()) 
# OK works
```


```python
# 04_05_hangman
#04_05_hangman_play
import random

words = ['chicken', 'dog', 'cat', 'mouse', 'frog']
lives_remaining = 14

def play():
	word = pick_a_word()
	while True:
		guess = get_guess(word)
		if process_guess(guess, word):
			print('You win! Well Done!')
			break
		if lives_remaining == 0:
			print('You are Hung!')
			print('The word was: ' + word)
			break

def pick_a_word():
	return random.choice(words)

def get_guess(word): # a stub: just simulates the players always guessing the letter a
	return 'a'
	
def process_guess(guess, word): # a stub: always assumes that the player guessed wrong and, thun, decreases lives_remaining by 1 and returns False to indicate that they didn't win.
	global lives_remaining # without this line, Python assumes that it is a new variable local to the functionl
	lives_remaining = lives_remaining -1
	return False
	
play()
```


```python
#04_06_hangman_get_guess

import random

words = ['chicken', 'dog', 'cat', 'mouse', 'frog']
lives_remaining = 14

def play():
	word = pick_a_word()
	while True:
		guess = get_guess(word)
		if process_guess(guess, word):
			print('You win! Well Done!')
			break
		if lives_remaining == 0:
			print('You are Hung!')
			print('The word was: ' + word)
			break

def pick_a_word():
	return random.choice(words)
	
def get_guess(word):
	print_word_with_blanks(word)
	print('Lives Remaining: ' + str(lives_remaining))
	guess = input(' Guess a letter or whole word?')
	return guess

def process_guess(guess, word):
	global lives_remaining
	lives_remaining = lives_remaining -1
	return False
	
def print_word_with_blanks(word): # a stub
	print('print_word_with_blanks: not done yet')
	
play()
```


```python
#04_07_hangman_print_word

import random

words = ['chicken', 'dog', 'cat', 'mouse', 'frog']
lives_remaining = 14
guessed_letters = ''

def play():
	word = pick_a_word()
	while True:
		guess = get_guess(word)
		if process_guess(guess, word):
			print('You win! Well Done!')
			break
		if lives_remaining == 0:
			print('You are Hung!')
			print('The word was: ' + word)
			break

def pick_a_word():
	return random.choice(words)
	
def get_guess(word):
	print_word_with_blanks(word)
	print('Lives Remaining: ' + str(lives_remaining))
	guess = input(' Guess a letter or whole word?')
	return guess

def process_guess(guess, word): # Curently, every time process_guess is called, it doesn't do anything with the guess because it's still astub. We can make it a bit less of a stub by having it add the guessed letter to guessed_letters.
	global lives_remaining
	global guessed_letters
	lives_remaining = lives_remaining - 1
	guessed_letters = guessed_letters + guess
	return False
	
def print_word_with_blanks(word):
	display_word = ''
	for letter in word:
		if guessed_letters.find(letter) > -1: # find function returns -1
			# letter found
			display_word = display_word + letter
		else:
			# letter not found
			display_word = display_word + '-'
	print(display_word)
	
play()
```


```python
# 04_08_hangman_full
import random

words=['chicken','dog','cat','mouse','frog']
lives_remaining=14
guessed_letters=''
def play():
    word=pick_a_word()
    while True:
        guess=get_guess(word)
        if process_guess(guess,word):
            print('You win! Well Done!')
            break
        if lives_remaining==0:
            print('You are Hung!')
            print('The wrod was: ' + word)
            break
def pick_a_word():
    return random.choice(words)

def get_guess(word):
    print_word_with_blanks(word)
    print('Lives Remaining: '+ str(lives_remaining))
    guess=input(' Guess a letter or whole word?')
    return guess

def print_word_with_blanks(word):
    display_word=''
    for letter in word:
        if guessed_letters.find(letter) > -1:
            #letter found
            display_word = display_word + '-'
        print(display_word)

def process_guess(guess,word):
    if len(guess) > 1:
        return whole_word_guess(guess, word)
    else:
        return single_letter_guess(guess, word)
    
def whole_word_gues(guess, word):
    global lives_remaining
    if guess == word:
        return True
    else:
        lives_remaining = lives_remaining - 1
        return False
    
def single_letter_guess(guess, word):
	global guessed_letters
	global lives_remaining
	if word.find(guess) == -1:
		# letter guess was incorrect
		lives_remaining = lives_remaining - 1
	guessed_letters = guessed_letters + guess
	if all_letters_guessed(word):
		return True
	return False
    
def all_letters_guessed(word):
    for letter in word:
        if guessed_letters.find(letter) == -1:
            return False
    return True

play()

```

    
    
    
    
    Lives Remaining: 14
     Guess a letter or whole word?aa
    
    
    
    
    Lives Remaining: 13
     Guess a letter or whole word?b
    
    
    
    
    Lives Remaining: 12
     Guess a letter or whole word?dog
    
    
    
    
    Lives Remaining: 11
     Guess a letter or whole word?cat
    
    
    
    
    Lives Remaining: 10
     Guess a letter or whole word?mouse
    
    
    
    
    Lives Remaining: 9
     Guess a letter or whole word?chicken
    
    
    
    
    Lives Remaining: 8
     Guess a letter or whole word?frog
    You win! Well Done!



```python
#04_08_hangman_full github
import random

words = ['chicken', 'dog', 'cat', 'mouse', 'frog']
lives_remaining = 14
guessed_letters = ''



def play():
	word = pick_a_word()
	while True:
		guess = get_guess(word)
		if process_guess(guess, word):
			print('You win! Well Done!')
			break
		if lives_remaining == 0:
			print('You are Hung!')
			print('The word was: ' + word)
			break
	
def pick_a_word():
	return random.choice(words)
	
def get_guess(word):
	print_word_with_blanks(word)
	print('Lives Remaining: ' + str(lives_remaining))
	guess = input(' Guess a letter or whole word?')
	return guess
	
def print_word_with_blanks(word):
	display_word = ''
	for letter in word:
		if guessed_letters.find(letter) > -1:
			# letter found
			display_word = display_word + letter
		else:
			# letter not found
			display_word = display_word + '-'
	print(display_word)

def process_guess(guess, word):
	if len(guess) > 1:
		return whole_word_guess(guess, word)
	else:
		return single_letter_guess(guess, word)

			
def whole_word_guess(guess, word):
	global lives_remaining
	if guess == word:
		return True
	else:
		lives_remaining = lives_remaining - 1
		return False

def single_letter_guess(guess, word):
	global guessed_letters
	global lives_remaining
	if word.find(guess) == -1:
		# letter guess was incorrect
		lives_remaining = lives_remaining - 1
	guessed_letters = guessed_letters + guess
	if all_letters_guessed(word):
		return True
	return False

def all_letters_guessed(word):
	for letter in word:
		if guessed_letters.find(letter) == -1:
			return False
	return True
	
play()
# Limitations
## case sensitive
## accident of "aa" should be "a"
```

    -----
    Lives Remaining: 14
     Guess a letter or whole word?DOG
    -----
    Lives Remaining: 13
     Guess a letter or whole word?MOUSE
    -----
    Lives Remaining: 12
     Guess a letter or whole word?mouse
    You win! Well Done!



```python
#04_08_hangman_full github + fix casesensitivity
import random

words = ['chicken', 'dog', 'cat', 'mouse', 'frog']
lives_remaining = 14
guessed_letters = ''



def play():
	word = pick_a_word()
	while True:
		guess = get_guess(word)
		# guess = lower(guess) # error
		guess = str.lower(guess) # error
		if process_guess(guess, word):
			print('You win! Well Done!')
			break
		if lives_remaining == 0:
			print('You are Hung!')
			print('The word was: ' + word)
			break
	
def pick_a_word():
	return random.choice(words)
	
def get_guess(word):
	print_word_with_blanks(word)
	print('Lives Remaining: ' + str(lives_remaining))
	guess = input(' Guess a letter or whole word?')
	return guess
	
def print_word_with_blanks(word):
	display_word = ''
	for letter in word:
		if guessed_letters.find(letter) > -1:
			# letter found
			display_word = display_word + letter
		else:
			# letter not found
			display_word = display_word + '-'
	print(display_word)

def process_guess(guess, word):
	if len(guess) > 1:
		return whole_word_guess(guess, word)
	else:
		return single_letter_guess(guess, word)

			
def whole_word_guess(guess, word):
	global lives_remaining
	if guess == word:
		return True
	else:
		lives_remaining = lives_remaining - 1
		return False

def single_letter_guess(guess, word):
	global guessed_letters
	global lives_remaining
	if word.find(guess) == -1:
		# letter guess was incorrect
		lives_remaining = lives_remaining - 1
	guessed_letters = guessed_letters + guess
	if all_letters_guessed(word):
		return True
	return False

def all_letters_guessed(word):
	for letter in word:
		if guessed_letters.find(letter) == -1:
			return False
	return True
	
play()
# Limitations
## case sensitive
## accident of "aa" should be "a"
```

    ---
    Lives Remaining: 14
     Guess a letter or whole word?AA
    ---
    Lives Remaining: 13
     Guess a letter or whole word?A
    ---
    Lives Remaining: 12
     Guess a letter or whole word?C
    ---
    Lives Remaining: 11
     Guess a letter or whole word?f
    ---
    Lives Remaining: 10
     Guess a letter or whole word?d
    d--
    Lives Remaining: 10
     Guess a letter or whole word?O
    do-
    Lives Remaining: 10
     Guess a letter or whole word?f
    do-
    Lives Remaining: 9
     Guess a letter or whole word?F
    do-
    Lives Remaining: 8
     Guess a letter or whole word?G
    You win! Well Done!



```python
help(str.lower)
```

    Help on method_descriptor:
    
    lower(...)
        S.lower() -> str
        
        Return a copy of the string S converted to lowercase.
    



```python
#04_08_hangman_full github + fix casesensitivity
import random

words = ['chicken', 'dog', 'cat', 'mouse', 'frog']
lives_remaining = 14
guessed_letters = ''



def play():
	word = pick_a_word()
	while True:
		guess = get_guess(word)
		# guess = lower(guess) # error
		guess = str.lower(guess) # error
		if process_guess(guess, word):
			print('You win! Well Done!')
			break
		if lives_remaining == 0:
			print('You are Hung!')
			print('The word was: ' + word)
			break
	
def pick_a_word():
	return random.choice(words)
	
def get_guess(word):
	print_word_with_blanks(word)
	print('Lives Remaining: ' + str(lives_remaining))
	guess = input(' Guess a letter or whole word?')
	
	return guess
	
def print_word_with_blanks(word):
	display_word = ''
	for letter in word:
		if guessed_letters.find(letter) > -1:
			# letter found
			display_word = display_word + letter
		else:
			# letter not found
			display_word = display_word + '-'
	print(display_word)

def process_guess(guess, word):
	if len(guess) > 1:
		return whole_word_guess(guess, word)
	else:
		return single_letter_guess(guess, word)

			
def whole_word_guess(guess, word):
	global lives_remaining
	if guess == word:
		return True
	else:
		lives_remaining = lives_remaining - 1
		return False

def single_letter_guess(guess, word):
	global guessed_letters
	global lives_remaining
	if word.find(guess) == -1:
		# letter guess was incorrect
		lives_remaining = lives_remaining - 1
	guessed_letters = guessed_letters + guess
	if all_letters_guessed(word):
		return True
	return False

def all_letters_guessed(word):
	for letter in word:
		if guessed_letters.find(letter) == -1:
			return False
	return True
	
play()
# Limitations
## accident of "aa" should be "a"
```
