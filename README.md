# Chess Legal Move Generator
The purpose of this project is to understand the importance of a test suite.
The project uses JUnit tests and includes the use of JaCoCo and IntelliJ's built-in static testing tools,
resulting in a code coverage rate of over 80%. The goal of this project is to demonstrate the significance 
of testing in software development and to showcase the various tools available to developers to help ensure the quality of their code.

## Description
This project takes in a chessboard configuration, specified by the positions of the chess pieces for both white and black players, as well as a piece to move. Using this information, the program generates a list of legal moves for the selected piece. The output is in the form of a string with the algebraic notation for each legal move.

For example, given the input "WHITE: Rf1, Kg1, Pf2, Ph2, Pg3
BLACK: Kb8, Ne8, Pa7, Pb7, Pc7, Ra5
PIECE TO MOVE: Rf1", the program will output "LEGAL MOVES FOR Rf1: e1, d1, c1, b1, a1".

## Run
1. Open the project in your preferred IDE (e.g., IntelliJ IDEA, Eclipse, etc.).
2. Ensure that you have JUnit and Jacoco installed in your IDE.
3. Open the test file (Main.java) and run it.
4. Modify the input strings according to your desired chessboard configuration. For example, you can use the following format:
```
WHITE: Rf1, Kg1, Pf2, Ph2, Pg3
BLACK: Kb8, Ne8, Pa7, Pb7, Pc7, Ra5
PIECE TO MOVE: Rf1
```
5. Review the output to see the list of legal moves for the piece.

**Note: This project assumes that the input is well-formed and follows the expected format. If the input is malformed or incorrect, the program may not function correctly.**

## Test Case

**BishopTest:** are designed to ensure that the getMoves() and validMove() methods of the Bishop class return the correct list of legal moves on an 8x8 chess board.

The tests cover various scenarios, such as when there are no pieces on the board, when there are pieces of the same color, when there are pieces of the opposite color, and when there are pieces blocking some moves. There are also edge cases tested, such as when there are obstacles on the board that may limit the legal moves of the Bishop. Overall, these tests help ensure the functionality and accuracy of the Bishop class in the larger Chess program.

**KingTest** The tests are designed to check if the King class and its methods work as intended in different scenarios, such as when the King is blocked by other pieces, or when it has no other pieces on the board to move to. The tests use JUnit assertions to compare expected results with actual results and make sure they match.

**KnightTest:** The KnightTest class contains unit tests for the Knight class. The tests verify the constructor and the getMoves method for different scenarios, including the presence of other chess pieces and the board boundaries. The tests use JUnit 5 and assert the expected and actual results.

**PawnTest:** The tests cover cases such as testing the constructor, testing legal moves for pawns with and without pieces blocking their way, testing if a pawn can move 1-2 steps depending on its position, and testing if a pawn can perform a double step if it hasn't moved yet. The tests use assertions to check that the actual results match the expected results.

**QueenTest:** It tests various scenarios for the getMoves() method of the Queen class, such as testing legal moves when there are no pieces on the board, testing moves when the Queen is blocked by a white piece, and testing moves when the Queen can capture an opponent's piece.

**RookTest:** The tests cover various scenarios where the rook can move legally or not on a board with other pieces. The tests verify that the expected legal moves are returned by the rook's getMoves() method.

**ValidCheckTest:** The tests include verifying the validity of input strings, checking whether the chess pieces are in check, and parsing input strings into an array. The test methods use assertions to check expected results against actual results.

**ChessBoardTest** : The tests cover methods for validating input, generating output, and creating chess pieces. The tests also check for expected behavior when null values are passed to the ChessBoard constructor.
## Junit Test
To run the JUnit tests for this project, follow these steps:

1. Open the project in IntelliJ IDEA.
2. Navigate to the test folder in the project explorer.
3. Right-click on the test folder and select "Run 'All Tests'".
4. Alternatively, you can run each test individually by right-clicking on a specific test class or method and selecting "Run".

## Coverage
To view coverage in IntelliJ IDEA using the default tool:

1.Open the project in IntelliJ IDEA.
2.Run the JUnit tests by right-clicking on the test class and selecting "Run <class name>".
3.After the tests are completed, click on the "Run" menu and select "Run '<class name>' with Coverage".
4.The coverage report will be displayed in the Coverage tab at the bottom of the screen.
Verify that the coverage is above 90%.

To view coverage using JaCoCo:
2.Run the command "mvn jacoco：report" to generate the coverage report.
The report can be found in the target/suite/jacoco/index.html.
Open the index.html file in a web browser to view the coverage report.

  
 Note: At the beginning, running Jacoco generated a report that tested all test cases with a coverage rate above 80%. However, after modifying the code, due to a configuration issue with Jacoco, only the Junit tests for ChessBoard and ValidCheck classes were executed. Even with only testing these two classes, the coverage rate remained above 80%. In the second modification, I tried to identify and modify the configuration issue, which resulted in only testing the Junit for the Chess class with a coverage rate above 80%.
 ## Not being implemented
 1. The program currently does not handle the case where all inputs are empty. During attempts to modify the program to handle this case, it was discovered that adjustments to the overall structure would be changed.
 2. The logic related to castling has not been implemented in the program.
 3. User input must strictly follow the required format, otherwise an error will occur.



 
