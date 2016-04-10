# CS110
Java Coding Example

/* OCP4_CountOccurance.java
 * Description: Counts the number of times a positive integer up to 100 occurs 
 * in a read-in list of no more than 10 numbers.  Displays the numbers and
 * each respective count in increasing order of the number; utilizes EOF.
 * Test Suite: More than 10 numbers in list, Negative numbers in list, Zeros in 
 * list, No numbers in list, Numbers above 100 in list, As requested list
 */

import java.util.Scanner;
import java.io.IOException;
import java.io.PrintWriter;
import java.io.FileReader;

public class OCP4_CountOccurance
{
  public static void main(String[] args) throws IOException
  {
    String fileName;
    String stgList[]=new String[10];
    int numList[]=new int[10];
    int cnt[]=new int[10];
    int i;
    int j;
    boolean excng;
    int str;
    
    fileName=FileName();
    Scanner infile = new Scanner(new FileReader(fileName));
    Scanner sc = new Scanner(System.in);
    
    while(infile.eof)  // <-- PROBLEM.
    {
    for(i=0;i<10;i++)
    {
      stgList[i]=infile.next();
      numList[i]=Integer.valueOf(stgList[i]);
    }
    for(i=0;i<10;i++)
    {
      do{
        excng=false;
        for(i=0;i<10;i++)
        {
          for(j=1;j<10;j++)
          {
            if(numList[i]>numList[j])
            {
              str=numList[i];
              numList[i]=numList[j];
              numList[j]=str;
              excng=true;
            }
          }
        }
      }while(excng);
    }
    cnt[i]=0;
    for(i=0;i<10;i++)
    {
      for(j=i+1;j<10;j++)
      {
        if(numList[i] == numList[j])
          cnt[i]++;
      }
    }
    System.out.println("Number /t Count");
    for(i=0;i<10;i++)
      System.out.println(numList[i]+" /t "+cnt[i]);
    infile.close();
    }
  }

  public static String FileName()
  {
    Scanner sc = new Scanner(System.in);
    
    String fileName;
    
    System.out.println("Enter the filename (with appropriate filetype) containing the list of values: ");
    fileName=sc.next();
    
    return fileName;
  }
}
