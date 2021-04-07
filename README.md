# Personal-projects
Random projects
Code for Sudoku Solver:-


public class test {
    static  int boxassigner(int i, int j) {
        if (i >= 0 && i <= 2) {
            if (j >= 0 && j <= 2) {
                return 1;
            } else if (j >= 3 && j <= 5) {
                return 2;
            } else {
                return 3;
            }
        }
        else if (i >= 3 && i <= 5) {
            if (j >= 0 && j <= 2) {
                return 4;
            } else if (j >= 3 && j <= 5) {
                return 5;
            } else {
                return 6;
            }
        }
        else{
            if (j >= 0 && j <= 2) {
                return 7;
            } else if (j >= 3 && j <= 5) {
                return 8;
            } else {
                return 9;
            }
        }
    }
    static boolean boxchecker(int [][] sudoku, int boxnum, int num){
        boolean f=true;
        if(boxnum == 1){
            for (int i = 0; i < 3; i++) {
                for (int j = 0; j < 3; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 2){
            for (int i = 0; i < 3; i++) {
                for (int j = 3; j < 6; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 3){
            for (int i = 0; i < 3; i++) {
                for (int j = 6; j < 9; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 4){
            for (int i = 3; i < 6; i++) {
                for (int j = 0; j < 3; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 5){
            for (int i = 3; i < 6; i++) {
                for (int j = 3; j < 6; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 6){
            for (int i = 3; i < 6; i++) {
                for (int j = 6; j < 9; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 7){
            for (int i = 6; i < 9; i++) {
                for (int j = 0; j < 3; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else if(boxnum == 8){
            for (int i = 6; i < 9; i++) {
                for (int j = 3; j < 6; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        else{
            for (int i = 6; i < 9; i++) {
                for (int j = 6; j < 9; j++) {
                    if (sudoku[i][j] == num) {
                        f = false;
                        break;
                    }
                }
            }
        }
        return f;
    }

    static boolean isSafe(int[][] sudoku, int num,int row,int col){
        boolean b1=true,b2=true,b3=true,b=false;
        int boxnum;
        for (int i = 0; i < 9; i++) {
            if (sudoku[row][i] == num) {
                b1 = false;
                break;
            }
        }
        for (int i = 0; i < 9; i++) {
            if(sudoku[i][col]==num){
                b2=false;
                break;
            }
        }
        boxnum=boxassigner(row,col);
        b3=boxchecker(sudoku,boxnum,num);
        if((b1==true)&&(b2==true)&&(b3==true)){
            b=true;
        }
        return  b;
    }
    static boolean solve(int [][] sudoku){
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if(sudoku[i][j]==0){
                    for (int k = 1; k < 10 ; k++){
                        if (isSafe(sudoku,k, i, j)){
                            sudoku[i][j] =k;
                            if(solve(sudoku)){
                                return true;
                            }
                            else{
                                sudoku[i][j]=0;
                            }
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    public static void main(String[] args) {
        int[][] sudoku = { {0,8,0,0,0,0,9,0,0},{0,0,0,7,0,0,1,0,0},{0,0,6,0,0,2,0,0,4},
                           {7,5,0,0,0,9,0,0,0},{0,0,0,0,0,0,0,0,6},{0,0,9,0,4,8,0,0,3},
                           {0,4,8,0,0,0,0,3,0},{0,0,0,0,1,0,0,0,0},{0,3,0,5,0,0,8,0,0} };
        boolean t=solve(sudoku);
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                System.out.print(sudoku[i][j] + "\t");
            }
            System.out.print("\n");
        }
    }
}
