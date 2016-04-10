# CS110
Java Coding Example

/* OCP5_MagicSquare.java
 * Description: Determines if a user-defined sequence of numbers is a "Magic Square" by 
 * placing it in a squate matrix, then comparing sums of lines to the "Magic Number".
 * Test Suite: 
 */

import java.util.Scanner;

public class OCP5_MagicSquare
{ 
  static final int rows=4;
  static final int columns=4;
  
  static final int listSize=16;
  
  public static void main(String[] args)
  {
    
    int[] list=new int[listSize];
    int[][] matrix=new int[rows][columns];
    
    list=createArithmeticSeq();
    matrix=matricize(list,matrix);
    printMatrix(matrix);
    matrix=reverseDiagonal(matrix);
    printMatrix(matrix);
    magicCheck(list,matrix);
  }
  
  public static int[] createArithmeticSeq()
  {
    Scanner sc=new Scanner(System.in);
    
    int first;
    int diff;
    int i;
    int list[]=new int[listSize];
    
    System.out.print("Enter the first number of the sequence: ");
    first=sc.nextInt();
    System.out.print("Enter the desired difference between numbers: ");
    diff=sc.nextInt();
    list[0]=first;
    for(i=1;i<listSize;i++)
      list[i]=list[i-1]+diff;
    
    return list;
  }
  
  public static int[][] matricize(int[] list,int[][] matrix)
  {
    int i;
    int j;
    int k;
    
    for(k=0;k<listSize;k++)
    {
      for(i=0;i<rows;i++)
      {
        for(j=0;j<columns;j++)
        {
          matrix[i][j]=list[k];
          k++;
        }
      }
    }
    
    return matrix;
  }
  
  public static int[][] reverseDiagonal(int[][] matrix)  // ***FIX ME***
  {
    int i;
    int j;
    int[][] locSvr=new int[rows][columns];
    
    for(i=0;i<(rows/2);i++)
    {
      j=i;
      locSvr[0][0]=matrix[i][j];
      matrix[i][j]=matrix[rows-(i+1)][columns-(j+1)];  //LftRgtDwn diagonal of 2D-array
      matrix[rows-(i+1)][columns-(j+1)]=locSvr[0][0];
    }
    j=columns-1;
    for(i=0;i<rows/2;i++)
    {
      locSvr[0][0]=matrix[i][j];
      matrix[i][j]=matrix[rows-(i+1)][i];  //RgtLftDwn diagonal of 2D-array
      matrix[rows-(i+1)][i]=locSvr[0][0];
      j--;
    }
    
    return matrix;
  }
  
  public static void magicCheck(int[] list,int[][] matrix)
  {
    int i;
    int j;
    int addEle=0;
    int mgcNum;
    int rowSum;
    int rowSumAr[]=new int[rows];
    int clmSum=0;
    int clmSumAr[]=new int[columns];
    int diagSum[]=new int[2];
    boolean rowEq=false;
    boolean clmEq=false;
    boolean diagEq=false;
    
    for(i=0;i<listSize;i++)
      addEle+=list[i];
    mgcNum=addEle/rows;   //Adds all elements of 1D-array, divides by number of rows/columns
    for(i=0;i<rows;i++)
    {
      rowSum=0;
      for(j=0;j<columns;j++)
        rowSum+=matrix[i][j];   //Adds each row of 2D-array
      rowSumAr[i]=rowSum;
    }
    for(j=0;j<columns;j++)
    {
      clmSum=0;
      for(i=0;i<rows;i++)
        clmSum+=matrix[i][j];   //Adds each column of 2D-array
      clmSumAr[j]=clmSum;
    }
    for(i=0;i<rows;i++)
    {
      diagSum[0]=0;
      j=i;
      diagSum[0]+=matrix[i][j];  //Adds LRD diagonal of 2D-array
    }
    diagSum[1]=0;
    i=0;
    for(j=columns-1;j>=0;j--)
    {
      diagSum[1]+=matrix[i][j];  //Adds RLD diagonal of 2D-array
      i++;
    }
    for(i=0;i<rows;i++)
    {
      if(mgcNum==rowSumAr[i])
        rowEq=true;
    }
    for(j=0;j<columns;j++)
    {
      if(mgcNum==clmSumAr[j])
        clmEq=true;
    }
    for(i=0;i<2;i++)
    {
      if(mgcNum==diagSum[i])
        diagEq=true;
    }
    if(rowEq && clmEq && diagEq)
      System.out.println("It is a magic square.");
    else
      System.out.println("It is not a magic square.");
  }
  
  public static void printMatrix(int[][] matrix)
  {
    int i;
    int j;
    
    for(i=0;i<rows;i++)
    {
      for(j=0;j<columns;j++)
      {
        System.out.print(" "+matrix[i][j]);
      }
      System.out.println();
    }
    System.out.println();
  }
}
