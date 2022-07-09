```python
test_board=['']*10
```


```python
from IPython.display import clear_output

def display_board(board):
    clear_output()  # Remember, this only works in jupyter!
    
    print('   |   |')
    print(' ' + board[7] + ' | ' + board[8] + ' | ' + board[9])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[4] + ' | ' + board[5] + ' | ' + board[6])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[1] + ' | ' + board[2] + ' | ' + board[3])
    print('   |   |')
       
```


```python
def player_input():
    marker = ''
    
    while not (marker == 'X' or marker == 'O'):
        marker = input('Player 1: Do you want to be X or O? ').upper()

    if marker == 'X':
        return ('X', 'O')
    else:
        return ('O', 'X')
        
        
```


```python
def place_marker(board, marker, position):
    
    board[position]=marker
    
```


```python
def win_check(board,mark):
    
    #WIN TIC TAC TOE?
    
    #NEED TO CHECK ALL ROWS and see if they all share the same marker
    return ((board[1]==board[2]==board[3]==mark) or
    (board[4]==board[5]==board[6]==mark) or
    (board[7]==board[8]==board[9]==mark) or
    
    #NEED TO CHECK ALL COLUMNS and see if they all share the same marker 
    (board[1]==board[4]==board[7]==mark) or
    (board[2]==board[5]==board[8]==mark) or
    (board[3]==board[6]==board[9]==mark) or
    
    #NEED TO CHECK DIAGONALS (2
    (board[5]==board[5]==board[9]==mark) or
    (board[3]==board[5]==board[7]==mark))
    
    
```


```python
import random 

def choose_first():
    flip=random.randint(0,1)
        
    if flip==0:
        return f'Player 1 will go first'
    else:
        return f'Player 2 will go first'
        
```


```python
def space_check(board, position):
    
   #Check if the space is available 
    return board[position]==' '
        
```


```python
def full_board_check(board):
    
    #Is my board full? If I have a space then my board is not full 
    for i in range(1,10):
        if space_check(board,i):
            return False 
        #Board is full if we return True 
    else:
        return True
```


```python
def player_choice(board):
    
    position=0
    
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board, position):
        position=int(input('Choose a position: (1-9)'))
    
    return position 
```


```python
def replay():
    
    choice='invalid'
    
    while choice not in ['Y', 'N']:
        choice= f'Would you like to play again (Y or N)?'
       
        
        if choice=='Y':
            return True
        else:
            return False
    
```


```python
print('Welcome to Tic Tac Toe')

while True:
    # Reset the board
    theBoard = [' '] * 10
    player1_marker, player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first.')
    
    play_game = input('Are you ready to play? Enter Yes or No.')
    
    if play_game.lower()[0] == 'y':
        game_on = True
    else:
        game_on = False

    while game_on:
        if turn == 'Player 1':
            # Player1's turn.
            
            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player1_marker, position)

            if win_check(theBoard, player1_marker):
                display_board(theBoard)
                print('Congratulations! You have won the game!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 2'

        else:
            # Player2's turn.
            
            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player2_marker, position)

            if win_check(theBoard, player2_marker):
                display_board(theBoard)
                print('Player 2 has won!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 1'

    if not replay():
        break
```

    Welcome to Tic Tac Toe
    


```python

```
