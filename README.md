# SUDOKU SOLVER -- ANUSHKA GAUR -202401100400043
Introduction

Sudoku is a logic-based number placement puzzle where the objective is to fill a 9x9 grid so that each row, each column, and each 3x3 subgrid contains all digits from 1 to 9 without repetition. Solving Sudoku puzzles manually can be time-consuming, and thus, an automated solver using Python can significantly enhance efficiency.

This report presents a Python-based Sudoku solver that employs the backtracking algorithm to solve puzzles efficiently. Additionally, a graphical user interface (GUI) is implemented using Tkinter to allow users to interactively input and solve Sudoku puzzles.
#CODE 
# Function to check if a number can be placed in a given cell
def is_valid(board, row, col, num):
    # Check if the number is not already in the current row
    for i in range(9):
        if board[row][i] == num:  # If the number is found in the row, return False
            return False
        # Check if the number is not already in the current column
        if board[i][col] == num:  # If the number is found in the column, return False
            return False
        # Check if the number is not already in the 3x3 subgrid
        if board[3 * (row // 3) + i // 3][3 * (col // 3) + i % 3] == num:
            return False
    return True  # Return True if the number is valid for the cell

# Function to solve the Sudoku puzzle using backtracking
def solve_sudoku(board):
    # Iterate over each cell in the grid
    for row in range(9):
        for col in range(9):
            if board[row][col] == 0:  # Check if the cell is empty
                # Try all numbers from 1 to 9
                for num in range(1, 10):
                    if is_valid(board, row, col, num):  # Check if the number is valid
                        board[row][col] = num  # Place the number in the cell
                        if solve_sudoku(board):  # Recursively attempt to solve the rest of the board
                            return True  # If successful, return True
                        board[row][col] = 0  # Backtrack by resetting the cell to empty
                return False  # If no number is valid, return False to backtrack
    return True  # Return True if the board is solved

# Function to print the Sudoku board
def print_board(board):
    for row in board:  # Loop through each row in the board
        # Print the row, replacing 0 with "." for empty cells
        print(" ".join(str(num) if num != 0 else "." for num in row))

# Example Sudoku puzzle with 0 representing empty cells
sudoku_board = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],  # Row 1
    [6, 0, 0, 1, 9, 5, 0, 0, 0],  # Row 2
    [0, 9, 8, 0, 0, 0, 0, 6, 0],  # Row 3
    [8, 0, 0, 0, 6, 0, 0, 0, 3],  # Row 4
    [4, 0, 0, 8, 0, 3, 0, 0, 1],  # Row 5
    [7, 0, 0, 0, 2, 0, 0, 0, 6],  # Row 6
    [0, 6, 0, 0, 0, 0, 2, 8, 0],  # Row 7
    [0, 0, 0, 4, 1, 9, 0, 0, 5],  # Row 8
    [0, 0, 0, 0, 8, 0, 0, 7, 9]   # Row 9
]

# Solve the puzzle and print the result
if solve_sudoku(sudoku_board):  # Check if a solution exists
    print("Solved Sudoku board:")  # Print success message
    print_board(sudoku_board)  # Display the solved board
else:
    print("No solution exists.")  # Print failure message if no solution is found
