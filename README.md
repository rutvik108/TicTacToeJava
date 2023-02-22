# TicTacToeJava
//import java.sql.ClientInfoStatus;
import java.util.*;

public class TicTacToe {
    static ArrayList<Integer> UserList=new ArrayList<>();
    static ArrayList<Integer> MonitorList=new ArrayList<>();

    public static void main(String[] args) {
        //create TicTacToe board
        char[][] board={
            {'+','-','+','-','+','-','+'},
            {'|',' ','|',' ','|',' ','|'},
            {'+','-','+','-','+','-','+'},
            {'|',' ','|',' ','|',' ','|'},
            {'+','-','+','-','+','-','+'},
            {'|',' ','|',' ','|',' ','|'},
            {'+','-','+','-','+','-','+'}
        };
        //print board for first time
        printboard(board);
        System.out.println();
        String  user="user";
        String monitor="monitor";
        while(true){
            //take input from the user
            Scanner sc=new Scanner(System.in);
            System.out.println("Enter value in range from 1 to 9");
            int userVal=sc.nextInt();
            //check for move is valid or not
            //put value on the board
            boolean check = putValue(board,userVal,"user");
            //if user enter override value or put out side the value than take value again
             while(!check){
                 System.out.println("oops ! you have entered wrong value");
                 System.out.println("please enter another value");
                 userVal=sc.nextInt();
                 check = putValue(board,userVal,"user");
             }
             //add value in list so it help to check winning conditions
            UserList.add(userVal);
             //print board after a move
            printboard(board);
            System.out.println();
             //now its turn for pc
            Random rand=new Random();
            //take random value from 1 to 9
            int cpuVal= rand.nextInt(9)+1;
            boolean pccheck = putValue(board,userVal,"monitor");
            //if user enter override value or put out side the value than take value again
            //in case of pc we not print any case
            while(!pccheck){
                cpuVal=rand.nextInt(9)+1;
                pccheck = putValue(board,cpuVal,"monitor");
            }
            //add value in list so it help to check winning conditions
            MonitorList.add(cpuVal);
            printboard(board);
            System.out.println();
            //check winning condition
            Boolean checks =winner();
            //if check is false means either win lose or draw we break the loop
            if(!checks){
                break;
            }
        }
    }
    public static Boolean winner(){
        List TopRow      = Arrays.asList(1,2,3);
        List MidRow      = Arrays.asList(4,5,6);
        List BottomRow   = Arrays.asList(7,8,9);
        List LeftCol     = Arrays.asList(1,4,7);
        List MidCol      = Arrays.asList(2,5,8);
        List RightCol    = Arrays.asList(3,6,9);
        List FirstCross  = Arrays.asList(1,5,9);
        List SecondCross = Arrays.asList(3,5,7);

        List<List<Integer>> WinningList=new ArrayList<>();
        WinningList.add(TopRow);
        WinningList.add(MidRow);
        WinningList.add(BottomRow);
        WinningList.add(LeftCol );
        WinningList.add(MidCol);
        WinningList.add(RightCol );
        WinningList.add(FirstCross);
        WinningList.add(SecondCross);
        //check winning conditions are match or not
        //list i because list contains list of list
        for(List i : WinningList){
           if(UserList.containsAll(i)){
               System.out.println("Congratulations ! You Won The Game !");
               return false;
            }
           else if(MonitorList.containsAll(i)){
               System.out.println("Oops You Lost ! Batter Luck Next Time.....");
               return false;
           }
           else if(UserList.size()+MonitorList.size()==9){
               System.out.println("oh ! it's a draw!.....");
           }
        }
        return true;
    }

    public static Boolean putValue(char [][] board,int userVal , String who) {
        //check user is playing or its computer turn
        char symbol;
        if(who.equals("user")){
           symbol='x';
        }
        else{
            symbol='O';
        }
        switch (userVal){
            case 1:
                if(board[1][1]=='x' || board[1][1] =='O'){
                    return false;
                }else
                board[1][1]=symbol;
                return true;
            case 2:
                if(board[1][3]=='x' || board[1][3] =='O'){
                    return false;
                }else
                board[1][3]=symbol;
                return true;
            case 3:
                if(board[1][5]=='x' || board[1][5] =='O'){
                    return false;
                }else
                board[1][5]=symbol;
                return true;
            case 4:
                if(board[3][1]=='x' || board[3][1] =='O'){
                    return false;
                }else
                board[3][1]=symbol;
                return true;
            case 5:
                if(board[3][3]=='x' || board[3][3] =='O'){
                    return false;
                }else
                board[3][3]=symbol;
                return true;
            case 6:
                if(board[3][5]=='x' || board[3][5] =='O'){
                    return false;
                }else
                board[3][5]=symbol;
                return true;
            case 7:
                if(board[5][1]=='x' || board[5][1] =='O'){
                    return false;
                }else
                board[5][1]=symbol;
                return true;
            case 8:
                if(board[5][3]=='x' || board[5][3] =='O'){
                    return false;
                }else
                board[5][3]=symbol;
                return true;
            case 9:
                if(board[5][5]=='x' || board[5][5] =='O'){
                    return false;
                }else
                board[5][5]=symbol;
                return true;
            default:
                return false;
        }
    }
    //print board
    public static void printboard(char[][] board){
        for (char[] chars : board) {
            for (char aChar : chars) {
                System.out.print(aChar);
            }
            System.out.println();
        }
    }

}
