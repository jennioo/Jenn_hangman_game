Title= """ create the hangman game having the ascii art of a hangman at the top. 
There should be an underscore as hint for where the letters will be filled.
when you fail your life reduces when you miss a letter it will give a comment(it should be dynamic).
Also when you there should be a dynamic comment
When you fail and game over you should print out the handman ascii art
When you guess a correct letter the letter should show in the right position of the 
"""     

hangman_art= """   
                              .........................................                            
                              .:+##################################+:..                             
                               -%@*++++++++++++++++++++++++++++++*@%-..                             
                               -%@=..                           .-@%-                               
                               -%@=.                            .-@%-                               
                               -%@=.                            .-@%-                               
                               -%@=.                           ..-@%-.. ..                          
                               -%@=.                        ..:*#%@@%#=....                         
                               -%@=.                      ...*@@#=--+%@%=..                         
                               -%@=.                      ..#@#:......-%@+.                         
                               -%@=.                      .=@@...     .+@%..                        
                               -%@=.                       =@@:.    ...+@%..                        
                               -%@=.                      ..#@%:.  ...=@@=..                        
                               -%@=.                      ...+@@%**%@@%-.. .                       
                               -%@=.                      .....-*@@@%+:....                         
                               -%@=.                            .-@%-...                            
                               -%@=.                          ..:%@@*:....                          
                               -%@=.                          .%@@@@@@+....                         
                               -%@=.                      ...#@@*=@%+#@@=....                       
                               -%@=.                     ..*@@#..-@%-.=%@@-..                       
                               -%@=.                   ..+@@#:...-@%-  .=@@@:...                    
                               -%@=.                   :#@%:.. ..-@%-  ...=@@*..                    
                               -%@=.                  ........  .-@%-    .......                    
                               -%@=.                   ......   .-@%-       ...                     
                               -%@=.                            .-@%-                               
                               -%@=.                           ..-@%-..                             
                               -%@=.                          ..=@@@%-...                           
                               -%@=.                          .#@%=+@@=...                          
                               -%@=.                      ....@@%:..-%@+...                         
                               -%@=.                   .. ..-@@#.....-%@#.. .                       
                               -%@=.                    ...+@@=..  ....#@%:..                       
                               -%@=.                   ...*@@-.    .....+@@=....                    
                               -%@=.                   .:#@#:.        ...=@@*...                    
                               -%@=.                  .:#@*:..           .:@@*..                    
                               -%@=.                   ......             ......                    
                               -%@=.                                                                
                               -%@=.                                                                
                               -%@=.                                                                
                               -%@=.                                                                
                     ...      .-%@=..                                                               
                     ..........-%@=.............................................                    
                   ..-*********#@@#*******************************************-..                   
                  ...=########################################################=.    
"""

import random
with open("5000_dictionary_words.txt") as file:
    final_words =[]
    words = file.readlines()
    for word in words:
        final_words.append(word.replace("\n",""))
    print(words[:2])   
    print(final_words[:2])

def hint(ran_w,guessed_letters):
    for h in ran_w:
        if h in guessed_letters:
            print(h,end=" ")
        else:
            print("_", end= " ")
    print()  
   
def wrong_guess():
    wrong_guesses =("Opps you have gueesed wrong", "Opps try again dummy", "Ahhh you failed this chance ", "You can do better this boy", "Think hard for once boy")
    return random.choice(wrong_guesses)
        
def right_guess():
    right_guesses =("Yess smart ass!", "Aren't you just incredible", "You can do it!", "I believe in you!", "Ouu smart guess!", "Boy o boy!", "I knew you were good!", "Great!", "Them dey call am superstar!", "Wow beautiful")
    return random.choice(right_guesses)
        

def main():
    global final_words
    lives=6
    guessed_letters =[]
     
    
    print("Welcome to the hangman game")
    print("Guess the word to save my life")
    print(f"You have {len(final_words)} to guess")
    

    ran_w= random.choice(final_words)
    

    while True:
        hint(ran_w, guessed_letters)
        user_guess = str(input("Enter your letter>>")).lower()

        if not user_guess.isalpha() or len(user_guess) != 1:
            print("Invalid input! input one letter")
            continue
        
        if user_guess in guessed_letters:
            print("You have already guessed this letter")
            continue
               

        guessed_letters.append(user_guess)


    
        if user_guess in ran_w:
            print (right_guess())
        else:
            print  (wrong_guess())
            lives -= 1
            print(f"You have {lives} live(s) left")

       

        if all(letter in guessed_letters for letter in ran_w):
           print(f"🎉 You guessed the word: {ran_w.upper()} \nYOU WIN!!!")
           final_words.remove(ran_w)
           break

        if lives == 0:
           print(f" Game Over! The word was:{ran_w.upper()}")
           print(hangman_art)
           final_words.remove(ran_w)
           break

main()

while True:

        user_play = input("Do you want to (P)lay again or (E)xit: ").lower()
        if user_play == "p":
            main()
        elif user_play =="e":
            print ("Goodbye!")
            break
        else:
            print("Invalid choice, please enter P or E")  
