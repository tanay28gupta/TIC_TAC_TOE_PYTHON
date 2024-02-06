# TIC_TAC_TOE_PYTHON
This repository contains a simple implementation of the classic Tic Tac Toe game using Python. The game is built using object-oriented programming principles and runs in the console/terminal.


import os
import time

board = [' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ']
player = 1
win_flags = {'Win': 1, 'Draw': -1, 'Running': 0, 'Stop': 1}
Game = win_flags['Running']
Mark = 'X'

# This Function Draws Game Board
def DrawBoard():
    print(" %c | %c | %c " % (board[1], board[2], board[3]))
    print("||_")
    print(" %c | %c | %c " % (board[4], board[5], board[6]))
    print("||_")
    print(" %c | %c | %c " % (board[7], board[8], board[9]))
    print("   |   |   ")

# This Function Checks if the position is empty or not
def CheckPosition(x):
    if board[x] == ' ':
        return True
    else:
        return False

# This Function Checks if a player has won or not
def CheckWin():
    global Game

    # Horizontal winning condition
    if (board[1] == board[2] and board[2] == board[3] and board[1] != ' ') or \
       (board[4] == board[5] and board[5] == board[6] and board[4] != ' ') or \
       (board[7] == board[8] and board[8] == board[9] and board[7] != ' '):
        Game = win_flags['Win']
    # Vertical Winning Condition
    elif (board[1] == board[4] and board[4] == board[7] and board[1] != ' ') or \
         (board[2] == board[5] and board[5] == board[8] and board[2] != ' ') or \
         (board[3] == board[6] and board[6] == board[9] and board[3] != ' '):
        Game = win_flags['Win']
    # Diagonal Winning Condition
    elif (board[1] == board[5] and board[5] == board[9] and board[5] != ' ') or \
         (board[3] == board[5] and board[5] == board[7] and board[5] != ' '):
        Game = win_flags['Win']
    # Match Tie or Draw Condition
    elif ' ' not in board[1:]:
        Game = win_flags['Draw']
    else:
        Game = win_flags['Running']

    print("Tic-Tac-Toe Game Designed By Sourabh Somani")
    print("Player 1 [X] --- Player 2 [O]\n")
    print()
    print()
    print("Please Wait...")
    time.sleep(3)

while Game == win_flags['Running']:
    os.system('cls' if os.name == 'nt' else 'clear')  # Clear the console screen
    DrawBoard()

    if player % 2 != 0:
        print("Player 1's chance")
        Mark = 'X'
    else:
        print("Player 2's chance")
        Mark = 'O'

    try:
        choice = int(input("Enter the position between [1-9] where you want to mark: "))
        if 1 <= choice <= 9 and CheckPosition(choice):
            board[choice] = Mark
            player += 1
            CheckWin()
        else:
            print("Invalid input. Please try again.")
            time.sleep(1)
    except ValueError:
        print("Invalid input. Please enter a number.")
        time.sleep(1)

os.system('cls' if os.name == 'nt' else 'clear')  # Clear the console screen
DrawBoard()

if Game == win_flags['Draw']:
    print("Game Draw")
elif Game == win_flags['Win']:
    player -= 1
    if player % 2 != 0:
        print("Player 1 Won")
    else:
        print("Player 2 Won")
