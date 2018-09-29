/*
 * Name:George Sayegh
 * Date: 9/28/18
 * Course Number: CSC-220
 * Course Name: Data Structures
 * Problem Number:3
 * Email: gsayegh13@gmail.com
 * Short Description of the Problem: Print the star pattern from provided data in .txt file
 */

import java.io.File;
import java.util.Scanner;
import java.io.FileNotFoundException;

public class Starpattern {
	
	// **********************************************
	
	//User input
	private static void processStardata(Scanner sc, String args[])
	
		throws FileNotFoundException 
	{
		System.out.println("Enter the full name of the Data file (Ex. StarData1.txt)");
		String filename = sc.nextLine();
		int data[][] = readStarData(filename);
		calculateStarData(data);
	}

	// **********************************************
	
	private static int[][] readStarData(String filename) 
	throws FileNotFoundException 
	{
		Scanner datafile = new Scanner(new File(filename));
		int rows = datafile.nextInt();
		int cols = datafile.nextInt();
		int data[][] = new int[rows][cols];
		
		for (int row = 0; row < data.length; row++) 
		{
			for (int col = 0; col < data[row].length; col++) 
			{
				data[row][col] = datafile.nextInt();
				System.out.printf("%3d", data[row][col]);

			}
			System.out.println();
		}
		return data;
	}

	// **********************************************
	
	private static void calculateStarData(int[][] data) 
	{
		int[][] checkStarData = new int[data.length][data[0].length];
		System.out.println("Calculated Data: ");
		System.out.println();
		for (int row = 1; row < data.length - 1; row++) 
		{
			for (int col = 1; col < data[row].length - 1; col++) 
			{
				for (int rowDelta = -1; rowDelta <= 1; rowDelta++) 
				{
					for (int colDelta = -1; colDelta <= 1; colDelta++) 
					{
					checkStarData[row][col] += data[row + rowDelta][col + colDelta];
					}
				}
				
			System.out.printf("%4d", checkStarData[row][col]);
			}
		
		System.out.println();
		}	
	createStarMap(checkStarData);
	}
	
	// **********************************************
	
	private static void createStarMap(int[][] checkStarData) 
	{
		char[][] starDataMap=new char[checkStarData.length][checkStarData[0].length];
			for(int i=0; i<checkStarData.length; i++) 
		{
				System.out.println("+------------------------------+");
				for(int j=0; j< checkStarData[i].length; j++) 
				{	
					if(checkStarData[i][j]/5.0 >6.0) //(array[i][j] + sum of the 8 surrounding intensities)/5 > 6.0
						starDataMap[i][j]='*';
					else
						starDataMap[i][j]='|';
					System.out.printf("%3c",starDataMap[i][j]);
				}
				System.out.println();
		}	
	}
	
	// **********************************************

	private static boolean doThisAgain(Scanner sc, String prompt) {

		System.out.print(prompt);
		String doOver = sc.nextLine();
		return doOver.equalsIgnoreCase("Y");
	}

	// **********************************************
	
	public static void main(String args[])

		throws FileNotFoundException {
		final String TITLE = "NASA Experimental Star Pattern program";
		final String CONTINUE_PROMPT = "Do this again? [y/n] ";
		System.out.println("Welcome to " + TITLE);
		Scanner sc = new Scanner(System.in);
		do {
			processStardata(sc, args);
		} while (doThisAgain(sc, CONTINUE_PROMPT));
		sc.close();
		System.out.println("Thank you for using " + TITLE);
	}
}
