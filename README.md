# snake-and-ladders
import random

def roll_dice():
    """Rolls a six-sided dice and returns the result."""
    return random.randint(1, 6)

def move_player(position, roll, snakes, ladders):
    """Moves the player based on dice roll, snakes, and ladders."""
    position += roll
    if position > 100:
        return position - roll  # Exceeding 100 doesn't count

    # Check for snakes or ladders
    if position in snakes:
        print(f"Oh no! Bitten by a snake at {position}. Going down to {snakes[position]}")
        position = snakes[position]
    elif position in ladders:
        print(f"Yay! Climbed a ladder at {position}. Going up to {ladders[position]}")
        position = ladders[position]

    return position

def snake_and_ladders():
    # Snakes and ladders positions
    snakes = {16: 6, 47: 26, 49: 11, 56: 53, 62: 19, 64: 60, 87: 24, 93: 73, 95: 75, 98: 78}
    ladders = {1: 38, 4: 14, 9: 31, 21: 42, 28: 84, 36: 44, 51: 67, 71: 91, 80: 100}

    # Initial positions of players
    players = {"Player 1": 0, "Player 2": 0}

    while True:
        for player in players:
            input(f"{player}'s turn. Press Enter to roll the dice...")
            roll = roll_dice()
            print(f"{player} rolled a {roll}")
            
            new_position = move_player(players[player], roll, snakes, ladders)
            print(f"{player} moved from {players[player]} to {new_position}")
            
            players[player] = new_position

            if players[player] == 100:
                print(f"Congratulations! {player} wins!")
                return

# Run the game
snake_and_ladders()
