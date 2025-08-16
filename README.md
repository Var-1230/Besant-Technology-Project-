import random

CHOICES = {'r': 'rock', 'p': 'paper', 's': 'scissors'}
WIN_PAIRS = {('r', 's'), ('p', 'r'), ('s', 'p')}  # first beats second

while True:
    user = input("Choose [r]ock, [p]aper, [s]cissors: ").strip().lower()
    if user not in CHOICES:
        print("Invalid choice. Please type r, p, or s.\n")
        continue    comp=random.choice(list(CHOICES.keys()))

    print(f"You: {CHOICIES[user]}  | Computer: {CHOICES[comp]}")
    if user == comp:
        print("Result: It's a tie!\n")
    elif (user, comp) in WIN_PAIRS:
        print("Result: You win!\n")
    else:
        print("Result: You lose!\n")

    again = input("Play again? (y/n): ").strip().lower()
    if again != 'y':
        print("Thanks for playing!")
        break
