import java.util.ArrayList;

public class Board
{
	int size;
	String[][] table;
	int numOfWhite;
	int numOfBlack;
	int forfeitCounter;
	
	int getForfeitCounter()
	{
		return forfeitCounter;
	}

	void setForfeitCounter(int count)
	{
		forfeitCounter=count;
	}
	
	public Board(int givenSize)
	{
		size = givenSize;
		table = new String[size][size];
		forfeitCounter=0;
		
		
		for(int i=0; i<size; i++)
		{
			for(int j=0; j<size; j++)
			{
				table[i][j]="| |";
			}
		}
		//default starting position
		table[size/2][size/2]="|w|";
		table[size/2-1][size/2-1]="|w|";
		table[size/2-1][size/2]="|b|";
		table[size/2][size/2-1]="|b|";

		numOfBlack=2;
		numOfWhite=2;
	}
	
	void showBoard()
	{
		System.out.print("  ");
		for(int i=0; i<size; i++)
		{
			System.out.print(" " + (char) ('a' + i) + " ");
		}
		for(int i=0; i<size; i++)
		{
			System.out.print("\n");
			System.out.print(i+1);
			System.out.print(" ");
			for(int j=0; j<size; j++)
			{
				System.out.print(table[i][j]);
			}
			System.out.print(" "+ (i+1));
			
		}
		System.out.print("\n");
		System.out.print("  ");
		for(int i=0; i<size; i++)
		{
			System.out.print(" " + (char) ('a' + i) + " ");
		}
		System.out.print("\n");
		System.out.println("Current score: Black : " + numOfBlack + " White: "+ numOfWhite);
	}
	
	ArrayList<String> getAvailableMoves(char colorChar)
	{
		
		ArrayList<String> moves = new ArrayList<String>();
		
		for(int i=0; i<size; i++)
		{
			for(int j=0; j<size; j++)
			{
				//find the opponent's positions
				if(table[i][j]!="| |" && table[i][j].charAt(1)!=(colorChar))
				{	
			
					int rowCheck;
					int columnCheck;
					for(int count=0; count<9; count++)
					{		
						
						rowCheck = i+(count/3)-1;
						columnCheck = j+((count%3)-1);
						
						//This will find all empty spaces adjactent to an opponent's color
						if(rowCheck>=0 && rowCheck<size && columnCheck>=0 && columnCheck<size)
						{
							if(table[rowCheck][columnCheck]=="| |")
							{
								if(outFlank(colorChar, (rowCheck), (columnCheck) ))
								{
									moves.add(intToChar(columnCheck)+Integer.toString((rowCheck)+1));
								}	
	
							}
						}					
					}
				}
			}
		}	
		//System.out.println(moves);
		return moves;
	}
	
	char intToChar(int num)
	{

		return (char) ('a' + num);
	}
	
	int charToInt(char column)
	{

		return (column - 'a');
	}
	
	boolean outFlank(char colorChar, int row, int column)
	{
		int rowCheck;
		int columnCheck;
		int nextRow;
		int nextCol;
		//8 possible directions to check: left and right along both row and column, and four diagonals
		for(int count=0; count<9; count++)
		{	

			rowCheck=row+(count/3)-1;
			columnCheck=column+((count%3)-1);
			
				while(rowCheck>=0 && rowCheck<size && columnCheck>=0 && columnCheck<size && table[rowCheck][columnCheck]!="| |" && table[rowCheck][columnCheck].charAt(1)!=colorChar)
				{
					nextRow=rowCheck+findDirection(rowCheck-row);
					nextCol=columnCheck+findDirection(columnCheck-column);
						
					if(nextRow>=0 && nextRow<size && nextCol>=0 && nextCol<size)
					{
						if(table[nextRow][nextCol].charAt(1)==colorChar)
						{
							return true;
						}
					}
					rowCheck=nextRow;
					columnCheck=nextCol;
				}				
		}			
		
		return false;
	}
	
	int findDirection(int check)
	{
		if(check==0)
			return 0;
		else if(check<0)
			return -1;
		else
			return 1;	
	}
		
	void updateBoard(String userMove, char colorChar)
	{
		//very similar to outflank method
		
		int row = Character.getNumericValue(userMove.charAt(1))-1;
		int column=charToInt(userMove.charAt(0));
		
		int rowCheck;
		int columnCheck;
		int nextRow;
		int nextCol;
		
		int updateRow;
		int updateCol;
		ArrayList<String> updates = new ArrayList<String>();
		//8 possible directions to check: left and right along both row and column, and four diagonals
		for(int count=0; count<9; count++)
		{	
			updates = new ArrayList<String>();

			rowCheck=row+(count/3)-1;
			columnCheck=column+((count%3)-1);
			
				
				while(rowCheck>=0 && rowCheck<size && columnCheck>=0 && columnCheck<size && table[rowCheck][columnCheck]!="| |" && table[rowCheck][columnCheck].charAt(1)!=colorChar)
				{
					nextRow=rowCheck+findDirection(rowCheck-row);
					nextCol=columnCheck+findDirection(columnCheck-column);
						
					updates.add(rowCheck+","+columnCheck);	
					if(nextRow>=0 && nextRow<size && nextCol>=0 && nextCol<size)
					{
						if(table[nextRow][nextCol].charAt(1)==colorChar)
						{
							for(int i=0; i<updates.size(); i++)
							{
								updateRow = Character.getNumericValue(updates.get(i).charAt(0));
								updateCol = Character.getNumericValue(updates.get(i).charAt(2));
								table[row][column]="|"+colorChar+"|";
								table[updateRow][updateCol]="|"+colorChar+"|";
								
								
							}
							//System.out.println(updates);
							if(colorChar=='b')
								{
									numOfBlack+=updates.size();
									numOfWhite-=updates.size();
								}
								else
								{
									numOfWhite+=updates.size();
									numOfBlack-=updates.size();
								}
							
							
						}
					}
					
					rowCheck=nextRow;
					columnCheck=nextCol;
								
				}	

		}
		
		if(colorChar=='b')
		{
			numOfBlack+=1;
			
		}
		else
		{
			numOfWhite+=1;
		}
		showBoard();
	
	}

	boolean gameOver()
		{
			if(forfeitCounter>1)
			{
				return true;
			}
			return false;
		}
		
		void getWinner()
		{
			if(numOfWhite>numOfBlack)
				System.out.print("Game Over, White is the winner!");
			else if(numOfBlack>numOfWhite)
				System.out.print("Game Over, Black is the winner!");
			else
				System.out.println("Game Over, it's a draw!");
		}
			
}
