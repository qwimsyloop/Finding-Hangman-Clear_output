# Inputting Syntax
import random
from IPython.display import clear_output

# Inputting the Drawing Output

Drawingframe = ["""
        _______
        |     |
        |     
        |
        |
        |
        |
        |___________
        |SAVE A LIFE|""", """

        _______
        |     |
        |     O
        |
        |
        |
        |
        |__________
        |TRY HARDER|""", """


        _______
        |     |
        |     O
        |   --|
        |
        |
        |
        |__________________________
        |STILL I KNOW YOU CAN DO IT|""", """


        _______
        |     |
        |     O
        |   --|--
        |
        |
        |
        |__________________________________
        |ITS NOT EASY FOR YOU BUT TRY AGAIN|""", """


         _______
        |     |
        |     O
        |   --|--
        |     |
        |    /
        |
        |____________________
        |DYING IS TIRING WORK|""", """


        _______
        |     |
        |     O
        |   --|--
        |     |
        |    /
        |
        |___________
        |LAST CHANCE|""", """


        _______
        |     |
        |    *_*
        |    /|\\
        |     |
        |    / \\
        |
        |________
        |GAME OVER|"""]


# inputting Variables for word guessing

def getRandomWord():
    words = ['apple', 'banana', 'mango', 'strawberry', 'orange', 'grape', 'pineapple', 'apricot',
             'lemon', 'coconut', 'watermelon', 'cherry', 'papaya', 'berry', 'peach', 'lychee', 'muskmelon']

    word = random.choice(words)
    return word

Wrongguesses = ''
Rightanswers = ''
secretWord = getRandomWord()

# Defining Functions and Parameters in this code chain

def Outputframe(Drawingframe, Wrongguesses, Rightanswers, secretWord):
    print(Drawingframe[len(Wrongguesses)])
    print("\n")

    print('Missed Letters:', end=' ')
    for letter in Wrongguesses:
        print(letter, end=' ')
    print("\n")

    blanks = '_' * len(secretWord)

# This replaces blanks with correctly guessed letters

    for i in range(len(secretWord)):
        if secretWord[i] in Rightanswers:
            blanks = blanks[:i] + secretWord[i] + blanks[i+1:]

# This shows the secret word with spaces in between each letter

    for letter in blanks:  
        print(letter, end=' ')
    print("\n")

    
# inputting the infinite loop Function

def getGuess(alreadyGuessed):
    while True:
        guess = input('Guess a letter for player ones word: ')
        guess = guess.lower()
        if len(guess) != 1:
            print('Please enter a single letter for player ones word.')      
        elif guess in alreadyGuessed:
            print('You have already guessed that letter for player ones word. Choose again.')           
        elif guess not in 'abcdefghijklmnopqrstuvwxyz':
            print('Please enter a single letter for player ones word.') 
        else:
            return guess
                
def playAgain():
    return input("\nDo you want to try again player 2? Just Type y or n - ").lower()
            
    
Wrongguesses = ''
Rightanswers = ''
secretWord = getRandomWord()
gameIsDone = False

while True:
    Outputframe(Drawingframe, Wrongguesses, Rightanswers, secretWord)

    guess = getGuess(Wrongguesses + Rightanswers)

    if guess in secretWord:
        Rightanswers = Rightanswers + guess

        foundAllLetters = True
        for i in range(len(secretWord)):
            if secretWord[i] not in Rightanswers:
                foundAllLetters = False
                break
        if foundAllLetters:
            print('\nYes! The secret word is "' +
                  secretWord + '"! You have won!')
            gameIsDone = True
    else:
        Wrongguesses = Wrongguesses + guess

        if len(Wrongguesses) == len(Drawingframe) - 1:
            Outputframe(Drawingframe, Wrongguesses,
                         Rightanswers, secretWord)
            print('You have run out of guesses!\nAfter ' + str(len(Wrongguesses)) + ' missed guesses and ' +
                  str(len(Rightanswers)) + ' correct guesses, the word was "' + secretWord + '"')
            gameIsDone = True

    if gameIsDone:
        if playAgain():
            Wrongguesses = ''
            Rightanswers = ''
            gameIsDone = False
            secretWord = getRandomWord()
            clear_output(wait=True)
        else:
            break
