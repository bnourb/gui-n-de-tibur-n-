# كود لعبة XO بلغة بايثون
def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 9)

def check_win(board, player):
    # تحقق من الصفوف والأعمدة
    for i in range(3):
        if all(cell == player for cell in board[i]) or \
           all(board[j][i] == player for j in range(3)):
            return True
    # تحقق من الأقطار
    if board[0][0] == board[1][1] == board[2][2] == player or \
       board[0][2] == board[1][1] == board[2][0] == player:
        return True
    return False

def check_draw(board):
    return all(cell != " " for row in board for cell in row)

def play_game():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"
    
    while True:
        print_board(board)
        print(f"اللاعب {current_player}، أدخل الصف والعمود (0-2) مفصولين بمسافة:")
        try:
            row, col = map(int, input().split())
            if board[row][col] == " ":
                board[row][col] = current_player
            else:
                print("الخانة مشغولة، جرب أخرى!")
                continue
        except (ValueError, IndexError):
            print("إدخال غير صالح، أدخل أرقاماً بين 0 و 2.")
            continue

        if check_win(board, current_player):
            print_board(board)
            print(f"🎉 مبروك! اللاعب {current_player} فاز!")
            break
        
        if check_draw(board):
            print_board(board)
            print("🤝 تعادل!")
            break
        
        current_player = "O" if current_player == "X" else "X"

if __name__ == "__main__":
    play_game()
