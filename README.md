# CS110
Java Coding Examples

 /* SlideTilePuzzle.java
 * Creates a 4x4 slide puzzle containing the numbers 1-15 and an open spot; a
 * chosen tile slides into the open spot.  Assume all inputted values are 
 * appropriate; user solves. (Note: Does not necessarily solve.)
 */

import java.util.Scanner;

public class SlideTilePuzzle
{
  public static void main(String[] args)
  {
    Scanner sc = new Scanner(System.in);
    
    int puz[][]=new int[4][4];
    int num;
    int i;
    int j;
    int tile;
    int tileLocX;
    int tileLocY;
    int spc;
    int spcLocX;
    int spcLocY;
    boolean posMv;
    int locSvr;
    char play;
    
    
    spc=0;
    tileLocX=0;
    tileLocY=0;
    spcLocX=0;
    spcLocY=0;

    
    for(num=0;num<=15;num++)
    {
      i=(int)(Math.random()*4);
      j=(int)(Math.random()*4);
      if(puz[i][j]==0)
        puz[i][j]=num;
      else
        num--;
    }
    
    // FIND SPACE (..technically don't need to do each time, but oh well.)
    for(i=0;i<4;i++)
    {
      for(j=0;j<4;j++)
      {
        if(spc==(puz[i][j]))
        {
          spcLocX=i;
          spcLocY=j;
        }
      }
    }
    
    
    
    
    // BEGIN LOOP
    do{
      
    printBoard(puz);
    System.out.print("Enter tile to move: ");
    tile=sc.nextInt();
    
    // FIND TILE
    for(i=0;i<4;i++)
    {
      for(j=0;j<4;j++)
      {
        if(tile==(puz[i][j]))
        {
          tileLocX=i;
          tileLocY=j;
        }
      }
    }
    
    
    
//    CHECK TILE LOCATION SENSIBLE (method tileMv)
    posMv=tileMv(tileLoc,spcLoc);
    while(posMv=false)
    {
      System.out.print("Invalid move.  Reenter tile to move: ");
      tile=sc.nextInt();
      for(i=0;i<4;i++)
      {
       for(j=0;j<4;j++)
        {
          if(tile==(puz[i][j]))
            tileLoc=puz[i][j];
        }
      }
      posMv=tileMv(tileLoc,spcLoc);
    }
    
    // MOVE TILE
    locSvr=puz[tileLocX][tileLocY];
    puz[tileLocX][tileLocY]=puz[spcLocX][spcLocY];
    puz[spcLocX][spcLocY]=locSvr;
    
    spcLocX=tileLocX;
    spcLocY=tileLocY;
    
  }while(!WIN(puz));
    // END LOOP
  }
  
  public static void printBoard(int board[][])
  {
    for(int i=0; i<4; i++)
    {
      System.out.print("|");
      for(int j=0; j<4; j++)
      {
        System.out.format("%2d",board[j][i]);
        System.out.print("|");
      }
      if(i!=3)
      System.out.println("\n--------------");
    }
    System.out.println();
  }
  
  public static boolean WIN(int puz[][])
  {
    boolean VOLCANO = true;
    
    for(int i = 0; i < 4; i++)
      for(int j = 0; j < 4; j++)
         if(puz[j][i]!=i*4+j)
            VOLCANO = false;
    
    return VOLCANO;
  }
    
  
  public static boolean tileMv(int tile,int spc)
  {
    boolean aprLoc;
    
    aprLoc=true;
    // CHECK TILE LOCATION SENSIBLE
    if()
    
   return aprLoc;
  }
}

