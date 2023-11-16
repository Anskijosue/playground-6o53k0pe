# Welcome!

This Java template lets you get started quickly with a simple one-page playground.

public static void main(String[] args) {
	// checks for custom play
	setPlay();
	//  sets full board to " "
	for(int row = 0; row < board.length; row++)
		for(int column = 0; column < board[row].length; column++)
			board[row][column] = " ";
	
	// prints an empty board for reference
	printBoard();
	game:
	while(true) {
		// 2 players
		for(int n = 0; n < 2; n++) {
			// gets a new play
			updateBoard(newRow(), newColumn());
			// prints the new board updated with the newest play
			printBoard();
			// checks if there is a winner
			if(checkForWinner()) {
				if(player)
					System.out.println("Player 1 wins!");
				else
					System.out.println("Player 2 wins!");
				break game;
			}
			// checks for a draw
			if(checkDraw()){
                System.out.println("You're all bad at this");
                break game;
            }
			// switches the players
			player = !player;
		}
		
	}
	
	
}

public static boolean checkForWinner() {
    String play = " ";
    boolean isWin = false;
    outerHorizontal:
    for(int a = 0; a < board.length; a++) {
        for(int b = 0; b < board[a].length - 3; b++) {
            play = board[a][b];
            if(play == " ")
                continue;
            if(board[a][b + 1] == play && board[a][b + 2] == play && board[a][b + 3] == play) {
                isWin = true;
                break outerHorizontal;
            }
                
        }
    }

    outerVertical:
    for(int x = 0; x < board.length - 3; x++) {
        for(int y = 0; y < board[x].length; y++) {
            play = board[x][y];
            if(play == " ")
                continue;
            if(board[x + 1][y] == play && board[x + 2][y] == play && board[x + 3][y] == play) {
                isWin = true;
                break outerVertical;
            }
        }
    }

    outerLeftDiagonal:
    for(int p = 0; p < board.length - 3; p++) {
        for(int o = 0; o < board[p].length - 3; o++) {
            play = board[p][o];
            if(play == " ")
                continue;
            if(board[p + 1][o + 1] == play && board[p + 2][o + 2] == play && board[p + 3][o + 3] == play) {
                isWin = true;
                break outerLeftDiagonal;
            }
        }
    }

    outerRightDiagonal:
    for(int u = 0; u < board.length - 3; u++) {
        for(int i = 3; i < board[u].length; i++) {
            play = board[u][i];
            if(play == " ")
                continue;
            if(board[u + 1][i - 1] == play && board[u + 2][i - 2] == play && board[u + 3][i - 3] == play) {
                isWin = true;
                break outerRightDiagonal;
            }
        }
    }

    return isWin;
}

public static boolean checkDraw() {
    for(int n = 0; n < board.length; n++) {
        for(int a = 0; a < board[n].length; a++) {
            if(board[n][a] == " ")
                return false;
        }
    }
    return true;
}

public static void updateBoard(int row, int column) {
	boolean notFinished = true;
	if(board[row][column] == " ") {
		if(player) {
			board[row][column] = p1;
		} else {
			board[row][column] = p2;
		}
		notFinished = false;
	}
	if(notFinished) {
		System.out.println("INVALID! Please try again.");
        updateBoard(newRow(), newColumn());
	}
}

public static int newRow() {
	System.out.print("What row? ");
	int row = in.nextInt();
	while(row < -4 || row > 4) {
		System.out.println("Invalid, Try again");
		System.out.print("What row? ");
		row = in.nextInt();
	}
	return  row + 4;
}

public static int newColumn() {
	System.out.print("What column? ");
	int column = in.nextInt();
	while(column < -4 || column > 4) {
		System.out.println("Invalid, Try again");
		System.out.print("What column? ");
		column = in.nextInt();
	}
	return  column + 4;
}

public static void printBoard() {
	System.out.println("    -4    -3    -2    -1     0     1     2     3     4");
	System.out.println("  +-----+-----+-----+-----+-----+-----+-----+-----+-----+");
    for(int n = board.length - 1; n >= 0; n--) {
        for(int x = 0; x < board[n].length; x++) {
            System.out.print("  |  " + board[n][x]);
        }
        System.out.println("  |  " + (n - 4));
        System.out.println("  +-----+-----+-----+-----+-----+-----+-----+-----+-----+");
    }
}

public static void setPlay() {
	if(p1 == "")
		p1 = "O";
	if(p2 == "")
		p2 = "X";
}
}

# Advanced usage

If you want a more complex example (external libraries, viewers...), use the [Advanced Java template](https://tech.io/select-repo/385)
