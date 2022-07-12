# Tic-Tac-Toe-Game
# display_board ,this method is used to setup the board 
def display_board(board):
    print(" "+  board[7]  +' | '+ " "+ board[8]+ " " +'|'+ " "+board[9])
    print("------------")
    print(" "+  board[4]  +' | '+ " "+ board[5]+ " " +'|'+ " "+board[6])
    print("------------")
    print(" "+  board[1]  +' | '+ " "+ board[2]+ " " +'|'+ " "+board[3])
    print("------------")
 
 
 # Player_input , this is used to choose the option that firt player want to enter X or O.
def player_input():
    marker = ""
    while marker !="X" and marker !="O":
        marker = input('Player 1 : Choose X or O : ').upper()
        
    if marker == 'X':
        return('X','O')
    else:
        return ('O','X')
        
     
def place_marker(board,marker,position):
    board[position]=marker
    
# win_check , in this function we check the condtion for wining the game    
def win_check(board,mark):
    return ((board[1]==mark and board[2]==mark and board[3]==mark) or
    (board[4]==mark and board[5]==mark and board[6]==mark) or
    (board[7]==mark and board[8]==mark and board[9]==mark) or
    (board[1]==mark and board[7]==mark and board[4]==mark) or
    (board[2]==mark and board[5]==mark and board[8]==mark) or
    (board[3]==mark and board[6]==mark and board[9]==mark) or
    (board[3]==mark and board[5]==mark and board[7]==mark) or
    (board[1]==mark and board[5]==mark and board[9]==mark)) 


# ramdom, it is used to assign that which player play first chance, to choose this we use random function
import random
def choose_first():
    flip = random.randint(0,1)
    if flip == 0:
        return 'Player 1'
    else:
        return 'Player 2'
 
 
 # this function is used to check blank space in the board.
def space_check(board,position):
    return board[position]==" "

def full_board_check(board):
    for i in range(1,10):
        if space_check(board,i):
            return False
    return True
    
 # this function is used to the input from the user , value of position    
def player_choice(board):
    position = 0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position = int(input('Choose a position from 1-9 : '))
    return position

# this function ask the user to play again or quit the game
def replay():
    choice= input("Play again ? Enter Yes or No")
    return choice=='Yes' or choice=='yes'

# main code of the program , in this we connect all the function that we have created above.
print('Welcome to TIC TAC TOE GAME')

while True:
    the_board=[' ']*10
    player1_marker,player2_marker= player_input()
    
    turn=choose_first()
    print(turn+'  Will go first')
    
    play_game=input('Are you ready to play? enter y or n')
    if play_game=='Y' or play_game=='y':
        game_on=True
    else:
        game_on=False
        
    while game_on:
        if turn=='Player 1':
            
            display_board(the_board)
            
            position=player_choice(the_board)
            
            place_marker(the_board,player1_marker,position)
            
            if win_check(the_board,player1_marker):
                display_board(the_board)
                print('Player 1 has won the game !')
                game_on=False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print('TIE GAME')
                    game_on=False
                else:
                    turn = "Player 2"
        else:
            display_board(the_board)
            
            position=player_choice(the_board)
            
            place_marker(the_board,player2_marker,position)
            
            if win_check(the_board,player2_marker):
                display_board(the_board)
                print('Player 2 has won the game !')
                game_on=False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print('TIE GAME')
                    game_on=False
                else:
                    turn = "Player 1"
                    
    
    

    
    
    
    
    if not replay():
        print('I hope you are enjoyed the game')
        break
