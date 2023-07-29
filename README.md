import java.util.Scanner;

public class TicTacToe {
    static char[][] board = new char[3][3];
    static char currentPlayer = 'X';

    // Initialize the board of TIC-TAC-TOE
   static void initializeBoard() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = '*';
            }
        }
    }

    // board display
    static void display() {
        for (int i = 0; i < 3; i++) {
            
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    // checking for overflow of board
    static boolean isFull() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == '*') {
                    return false;
                }
            }
        }
        return true;
    }

    // winning of a player
    private static boolean checkWin() {
        return (checkRows() || checkColumns() || checkDiagonals());
    }

    // checking for all rows
    private static boolean checkRows() {
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != '*') {
                return true;
            }
        }
        return false;
    }

    // checking for all columns
    private static boolean checkColumns() {
        for (int i = 0; i < 3; i++) {
            if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != '*') {
                return true;
            }
        }
        return false;
    }

    // checking for both the diagnols
    private static boolean checkDiagonals() {
        return ((board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != '*')
                || (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != '*'));
    }

    // placing the values of player moves
    private static void placeMove(int row, int col) {
        if (board[row][col] == '*') {
            board[row][col] = currentPlayer;
        } else {
            System.out.println("Cell is already occupied. Try again!");
        }
    }

    // switching of player from X to O and from O to X
    private static void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        initializeBoard();

        System.out.println("-----------TIC-TAC-TOE-----------");
        display();

        while (!checkWin() && !isFull()) {
            System.out.println("Player " + currentPlayer + ", Enter row and column number");
            int row = s.nextInt();
            int col = s.nextInt();

            placeMove(row, col);
            display();
            switchPlayer();
        }

        if (checkWin()) {
            switchPlayer();
            System.out.println("Player " + currentPlayer + " wins!!!");
        } else {
            System.out.println("It's a draw! The game is over.");
        }

    }
}
