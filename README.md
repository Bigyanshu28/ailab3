# Chess AI with Minimax (Python)

## Problem Statement
This project implements a **Chess game AI** using the **Minimax algorithm**.  
- The AI evaluates moves by looking ahead a few turns (default search depth = 3).  
- The human player can choose to play as **White (first)** or **Black (second)**.  
- The AI plays legal moves only and tries to maximize its advantage.  

---

## Approach
1. **Board Representation**:  
   - Uses the [`python-chess`](https://pypi.org/project/chess/) library for board setup, move generation, and game rules.  

2. **Evaluation Function**:  
   - Assigns material values to pieces:  
     - Pawn = 1  
     - Knight = 3  
     - Bishop = 3  
     - Rook = 5  
     - Queen = 9  
     - King = 0 (not scored, since losing the king ends the game)  
   - Score = (White material − Black material).  
   - Special handling:  
     - **Checkmate**: ±9999  
     - **Stalemate / Insufficient Material**: 0  

3. **Minimax Algorithm**:  
   - Explores all legal moves up to a given depth.  
   - **Maximizing Player**: AI, tries to maximize score.  
   - **Minimizing Player**: Opponent, tries to minimize score.  

4. **Best Move Selection**:  
   - Iterates over all possible moves for AI.  
   - Chooses the move with the highest evaluation after running Minimax.  

5. **Game Loop**:  
   - Human player makes moves in **UCI format** (e.g., `e2e4`).  
   - AI responds with its calculated best move.  
   - Game continues until **checkmate, stalemate, or draw**.  

---

## Implementation Details
- **`evaluate_board(board)`** → Evaluates board based on material balance and endgame conditions.  
- **`minimax(board, depth, maximizing)`** → Recursively explores possible future moves.  
- **`find_best_move(board, depth)`** → Finds the AI’s best move using Minimax.  
- **`play_game()`** → Handles the interactive game loop with user input and AI responses.  

---     

## Time Complexity
- Minimax explores **O(b^d)** states:  
  - b = branching factor (~35 average legal moves in chess).  
  - d = search depth (default = 3).  
- Worst-case: **O(35^3) ≈ 42,875 evaluations**.  

## Space Complexity
- **O(d)** recursion depth (stack).  
- Board state handled by `python-chess`.  

---

## Use Cases
- Demonstrates **AI decision-making in board games**.  
- Educational tool for **game theory, recursion, and adversarial search**.  
- Can be extended with **Alpha-Beta pruning, heuristics, and deeper searches**.  

---

## Limitations
- **No Alpha-Beta pruning** → AI explores all moves, making it slow at higher depths.  
- **Evaluation function is simple** → Only counts material, ignores positioning, pawn structure, king safety, etc.  
- **Limited depth (3 by default)** → Cannot see far-ahead tactics or strategies.  


# Tic-Tac-Toe with Minimax AI (C++)

## Problem Statement
This project implements a **Tic-Tac-Toe game** where a human can play against an **AI powered by the Minimax algorithm**.  
- The board is a 3×3 grid.  
- The AI plays optimally, ensuring it never loses.  
- The player can choose whether the AI plays as **X (first)** or **O (second)**.

---

## Approach
1. **Board Representation**:  
   - The board is stored as a vector of size 10 (index 1–9 used).  
   - Empty cells are represented by **2**.  
   - X is represented by **3**, O is represented by **5**.  
   - Winning lines are detected using the **product trick**:
     - 3 × 3 × 3 = 27 → X wins  
     - 5 × 5 × 5 = 125 → O wins  

2. **Minimax Algorithm**:  
   - Recursively evaluates all possible moves until the game reaches a win, loss, or draw.  
   - **Maximizing player** = AI, tries to maximize score.  
   - **Minimizing player** = Human, tries to minimize score.  
   - Scoring:  
     - AI win = `+10 - depth`  
     - Human win = `-10 + depth`  
     - Draw = 0  

3. **Game Loop**:  
   - If AI’s turn, it uses Minimax to choose the best move.  
   - If Human’s turn, user is prompted to input a move (1–9).  
   - After each move, the board is printed.  
   - The game ends when either player wins or the board is full (draw).  

---

## Implementation Details
- **`printBoard()`** → Prints the current board.  
- **`checkWinner()`** → Checks if either X or O has won.  
- **`isFull()`** → Checks if the board is completely filled.  
- **`minimax()`** → Recursive function that evaluates moves and assigns scores.  
- **`aiMove()`** → AI finds and plays the best move using Minimax.  
- **`humanMove()`** → Accepts valid input from the human player.  
- **`main()`** → Handles setup, turn-taking, and game result display.  

---


## Time Complexity
- The Tic-Tac-Toe board has at most 9! possible game states.  
- Minimax explores all possible moves: **O(b^d)** where:  
  - b = branching factor (≤ 9)  
  - d = depth of game tree (≤ 9)  
- In worst case: **O(9!) ≈ 362,880 states** (manageable).  

## Space Complexity
- **O(d)** = O(9), due to recursion depth.  
- Board state stored globally.  

---

## Use Cases
- Classic AI demonstration of **Minimax algorithm**.  
- Educational tool for **game theory and decision-making**.  
- Useful for teaching **recursion, backtracking, and adversarial search**.  

---

## Limitations
- **Fixed to Tic-Tac-Toe** (not scalable to larger boards like 4×4).  
- **No alpha-beta pruning** → explores all states, though pruning could optimize.  
- **Blocking vs winning is not weighted differently** (pure Minimax evaluation).  
