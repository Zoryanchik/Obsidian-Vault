```c
#include <stdio.h> 
#include <stdlib.h>
#include <time.h>

class Dice {
public:
    int numSides;
    int roll();
};

int Dice::roll() {
    return rand() % numSides + 1;
}

class Player {
public:
    char* name;
    int makeGuess();
};

int Player::makeGuess() {
    int guess;
    printf("%s, make a guess (between 1 and 6): ", name);
    scanf("%d", &guess);
    return guess;
}

int main() {
    srand(static_cast<unsigned int>(time(nullptr)));

    Dice sixSidedDice;
    sixSidedDice.numSides = 6;

    Player player1;
    player1.name = "Player 1";

    int guess = player1.makeGuess();
    int rollResult = sixSidedDice.roll();

    if (guess == rollResult) {
        printf("Congratulations! %d is correct. You win!\n", guess);
    } else {
        printf("Sorry, %d is incorrect. The correct answer is %d. Try again!\n", guess, rollResult);
    }

    return 0;
}
void printResult(int rolled_number) {
if (guess == rolled_number)
std::cout << "Lucky you! You WON!\n";
else
std::cout << "Better luck next time! The dice rolled " << rolled_number << ".\n"; 
} 




