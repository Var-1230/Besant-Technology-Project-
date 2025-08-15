# Besant-Technology-Project-
Stone papper sissor
import random
import os
import numpy as np

# ------------------ CONSTANTS & VARIABLES ------------------
CHOICES = ["rock", "paper", "scissors"]  # list
WIN_RULES = {  # dictionary
    "rock": "scissors",
    "paper": "rock",
    "scissors": "paper"
}

# ------------------ GENERATOR FUNCTION ------------------
def result_generator(results):
    for res in results:
        yield res

# ------------------ GAME CLASS ------------------
class RockPaperScissors:
    def __init__(self, rounds=3):
        self.rounds = rounds
        self.user_score = 0
        self.computer_score = 0
        self.results = []  # list to store match outcomes
    
    def get_user_choice(self):
        try:
            choice = input("Enter rock, paper, or scissors: ").lower().strip()
            if choice not in CHOICES:
                raise ValueError("Invalid choice! Please type rock, paper, or scissors.")
            return choice
        except ValueError as e:
            print(e)
            return self.get_user_choice()

    def get_computer_choice(self):
        return random.choice(CHOICES)

    def decide_winner(self, user, computer):
        if user == computer:
            return "Draw"
        elif WIN_RULES[user] == computer:
            self.user_score += 1
            return "User Wins"
        else:
            self.computer_score += 1
            return "Computer Wins"

    def play_round(self):
        user_choice = self.get_user_choice()
        comp_choice = self.get_computer_choice()
        print(f"Computer chose: {comp_choice}")
        result = self.decide_winner(user_choice, comp_choice)
        print(f"Result: {result}")
        self.results.append((user_choice, comp_choice, result))  # tuple

    def save_results(self, filename="game_results.txt"):
        with open(filename, "w") as file:
            for user, comp, res in self.results:
                file.write(f"User: {user}, Computer: {comp}, Result: {res}\n")
        print(f"Results saved in {os.path.abspath(filename)}")

    def show_final_score(self):
        scores = np.array([self.user_score, self.computer_score])
        print(f"Final Scores -> User: {self.user_score}, Computer: {self.computer_score}")
        print(f"Average Score: {np.mean(scores):.2f}")

    def start_game(self):
        print("🎮 Welcome to Rock-Paper-Scissors 🎮")
        for _ in range(self.rounds):
            self.play_round()
        self.show_final_score()
        self.save_results()

# ------------------ LAMBDA EXAMPLE ------------------
uppercase_choice = lambda x: x.upper()

# ------------------ MAIN EXECUTION ------------------
if __name__ == "__main__":
    game = RockPaperScissors(rounds=3)
    game.start_game()

    # Using generator to show match history
    print("\nGame History:")
    for outcome in result_generator(game.results):
        print(outcome)

    # Lambda demo
    print("\nSample Lambda Output:", uppercase_choice("rock"))
