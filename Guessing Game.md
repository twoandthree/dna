#Steven Johnston
#06/9/2018
#Guessin Game
#This program creates are guessing game.

#This program creates a guessing game where player 1 inputs a number, and player
#2 attempts to guess it correctly. The program prompts player 2 for the correct
#number, and the player may guess indefinetely until the player guesses corretly.
#After the game, player 2 receives statistics about his game, including:
#the amount of guesses it took to get the right number, and all the guesses the
#player used.

CAP = 100


def intro():
    #This function welcomes the user to the game.
    
    print("Welcome to the guessing game!")
    print()
    

def guessing_game():
    #This function allows player 1 to input a number. Next player 2 must guess the number.
    #A while loop is utilized to indefinitely prompt player 2 for the right number
    #until the player has guesses correctly. The guesses, and tries are documented in
    #an empty list, and count variable respectively. Lastly, those two are returned
    #into the function stats to report to the player their statistics of the game.
    
    stats = []
    tries = 0
    
    player_one = int(input("Player 1: Enter number for Player 2 to guess between 0 and 100: "))
    
    while player_one < 0 or player_one > CAP:
        player_one = int(input("Player 1: Enter number for Player 2 to guess between 0 and 100: "))
    print()

    player_two = int(input("Player 2, guess a number: "))
    stats.append(player_two)
    
    if player_two == player_one:
        print("You go it right in 1 guess! Wow, you are AMAZING.")       

    while player_two != player_one:
        if player_two > player_one:
            print("Too high...")
            player_two = int(input("Player 2, guess a number: "))
            stats.append(player_two)
            tries += 1
        elif player_two < player_one:
            print("Too low...")
            player_two = int(input("Player 2, guess a number: "))
            stats.append(player_two)
            tries += 1
    else: 
        print("Correct!")
        tries += 1

        stats.append(tries)
    print()

    return stats


def stats(player_stats):
    #This function takes in the statistics from the function guessing game as a
    #parameter. I utilize an empty string, and add all the guesses into the string
    #to print them out properly.
    
    guesses = " "
    
    print("It took you", player_stats[-1], "tries to guess correctly!")
    player_stats.pop()

    for stat in range(0, len(player_stats)):
        guesses += str(player_stats[stat]) + " "
    print("The numbers you guesses were:" + guesses)
    pass
    

def main():
    intro()
    statistics = guessing_game()
    
main()

