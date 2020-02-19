# Study
### 2020-02-17
- [Backtracking](https://leetcode.com/explore/learn/card/recursion-ii/472/backtracking/2654/)

### 2020-02-19
- [Unsuccessful Problom](https://leetcode.com/problems/sudoku-solver/)
```
class Solution {

    public static void main(String[] args) {
        Solution s = new Solution();
        char[][] board = new char[][]
                {{'5','3','.','.','7','.','.','.','.'},{'6','.','.','1','9','5','.','.','.'},{'.','9','8','.','.','.','.','6','.'},{'8','.','.','.','6','.','.','.','3'},{'4','.','.','8','.','3','.','.','1'},{'7','.','.','.','2','.','.','.','6'},{'.','6','.','.','.','.','2','8','.'},{'.','.','.','4','1','9','.','.','5'},{'.','.','.','.','8','.','.','7','9'}};

        s.solveSudoku(board);
    }

    public void solveSudoku(char[][] board) {
        bk(board, 0, 0 );
    }

    public boolean bk(char[][] board, int row, int col) {
        if(row > 9) {
            return true;
        }
        if(col > 8) {
            return bk(board, row+1, 0);
        }
        if(board[row][col] != '.') {
            return bk(board, row, col + 1);
        }
        char[] map = new char[] {'0','1', '2', '3','4','5','6','7','8','9'};
        for(int i = 1; i < 10; i++) {
            if(check(board, map[i] , row, col)) {
                board[row][col] = map[i];
                if(!bk(board, row, col + 1)) {
                    board[row][col] = '.';
                } f

            }
        }

        return false;
    }

    public boolean check(char[][] board, char val, int row, int col) {
        if(!checkBox(board, val, row, col)) {
            return false;
        }

        return checkEach(board, val, row, col, +1, 0) && checkEach(board, val, row, col, 0, +1);
    }

    public boolean checkBox(char[][] board,
                            int val,
                            int row,
                            int col) {
        int[][] boxRow = new int[][]{
                {0,0,0, 0,0,0,0,0,0}
                ,{0,0,0, 0,0,0,0,0,0}
                ,{0,0,0, 0,0,0,0,0,0}
                ,{2,2,2,2,2,2,2,2,2}
                ,{2,2,2,2,2,2,2,2,2}
                ,{2,2,2,2,2,2,2,2,2}
                ,{6,6,6,6,6,6,6,6,6}
                ,{6,6,6,6,6,6,6,6,6}
                ,{6,6,6,6,6,6,6,6,6}
        };
        int[][] boxCol = new int[][]{
                {0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
                ,{0,0,0,3,3,3,6,6,6}
        };

        int iE = boxRow[row][col]+3;
        int jE = boxCol[row][col]+3;
        for(int i = boxRow[row][col]; i < iE; i++ ) {
            for(int j = boxCol[row][col] ; j< jE; j++ ) {
                if(board[i][j] == val) {
                    return false;
                }
            }
        }
        return true;
    }

    public boolean checkEach(char[][] board,
                             char val,
                             int row,
                             int col,
                             int plusRow,
                             int plusCol) {
        if(row > board.length -1 ||
                row < 0 ||
                col > board[row].length -1 ||
                col < 0) {
            return true;
        }

        if(board[row][col] == val) {
            return false;
        }

        return checkEach(board, val, row+plusRow, col + plusCol, plusRow, plusCol);
    }


} 
```
