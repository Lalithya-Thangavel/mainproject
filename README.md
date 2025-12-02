# mainproject



{
import java.util.*;

public class PlayfairEncrypt {
    static char[][] m = {
        {'L','G','D','B','A'},
        {'Q','M','H','E','C'},
        {'U','R','N','I','F'},
        {'X','V','S','O','K'},
        {'Z','Y','W','T','P'}
    };

    static int[] pos(char c){ 
        for(int i=0;i<5;i++) for(int j=0;j<5;j++) 
            if(m[i][j]==c) return new int[]{i,j}; 
        return null; 
    }

    static String enc(String t){
        t=t.toUpperCase().replaceAll("[^A-Z]","").replace("J","I");
        StringBuilder r=new StringBuilder();
        for(int i=0;i<t.length();i+=2){
            char a=t.charAt(i), b=(i+1<t.length())?t.charAt(i+1):'X';
            if(a==b) b='X';
            int[] A=pos(a), B=pos(b);
            if(A[0]==B[0]) r.append(m[A[0]][(A[1]+1)%5]).append(m[B[0]][(B[1]+1)%5]);
            else if(A[1]==B[1]) r.append(m[(A[0]+1)%5][A[1]]).append(m[(B[0]+1)%5][B[1]]);
            else r.append(m[A[0]][B[1]]).append(m[B[0]][A[1]]);
        }
        return r.toString();
    }

    public static void main(String[] a){
        String msg="the house is being sold tonight";
        System.out.println("Encrypted: "+enc(msg));
    }
}
}
OUTPUT:
Encrypted: WECEXIOHNOEIFIDVXBBWSIRBEW
