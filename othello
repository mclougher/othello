public class othello
{
	public static void main(String[] args)
	{
		Player playerOne = new Player("Black",'b');
		Player playerTwo = new Player("White",'w');
		
		//8x8 board, could scale up/down size by changing parameter here
		Board gameBoard = new Board(8);
		gameBoard.showBoard();
		
		while(!gameBoard.gameOver())
		{
			playerOne.makeMove(gameBoard);
			playerTwo.makeMove(gameBoard);
		}
		
		gameBoard.getWinner();	
		
	}

}
