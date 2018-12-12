import java.util.Scanner;
import java.util.ArrayList;

public class Player
{
	String color;
	char colorChar;
	
	public Player(String color, char colorChar)
	{
		this.color=color;
		this.colorChar=colorChar;
	}
	
	boolean makeMove(Board gameBoard)
	{		
		ArrayList<String> moves = gameBoard.getAvailableMoves(colorChar);
		
		Scanner sc = new Scanner(System.in);
		if(moves.size()==0)
		{	
			System.out.print("No available moves, " + this.color + ", you must forfeit your turn! \n");
			gameBoard.setForfeitCounter(gameBoard.getForfeitCounter()+1);
		}
		else
		{
			gameBoard.setForfeitCounter(0);
			System.out.print(this.color + ", please make a move: ");
			String input = sc.next();
			
			if(!moves.contains(input))
			{
				System.out.print("Sorry, " + this.color + ", that is not a valid move: \n");
				makeMove(gameBoard);
			}
			else
			{
				gameBoard.updateBoard(input, this.colorChar);
				
			}
		}	
		
		return true;
	}

}
