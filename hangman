#include <iostream>
#include <vector>
#include <string>
#include <cstdlib>
#include <ctime>
#include <algorithm>

class HangmanGame {
private:
    std::vector<std::string> wordList;
    std::string secretWord;
    std::string guessedWord;
    std::vector<char> wrongGuesses;
    int maxAttempts;

    void initializeWordList() {
        wordList = {"soccer", "basketball", "tennis", "cricket", "rugby", "hockey", "baseball",
                    "volleyball", "golf", "boxing", "wrestling", "swimming", "cycling",
                    "badminton", "gymnastics", "skating", "skiing", "surfing", "karate",
                    "judo", "taekwondo", "sailing", "archery", "fencing", "rowing", "diving",
                    "handball", "equestrian", "weightlifting", "triathlon", "motorsport",
                    "climbing", "polo", "darts", "snooker", "bowling", "billiards", "lacrosse",
                    "softball", "curling", "squash", "racquetball", "pingpong", "kendo",
                    "sumo", "biathlon", "pentathlon", "canoeing", "bobsleigh", "luge"};
    }

    void chooseRandomWord() {
        srand(static_cast<unsigned int>(time(0)));
        int index = rand() % wordList.size();
        secretWord = wordList[index];
        guessedWord = std::string(secretWord.size(), '_');
    }

public:
    HangmanGame() : maxAttempts(7) {
        initializeWordList();
        chooseRandomWord();
    }

    void displayStatus() const {
        std::cout << "Guessed word: " << guessedWord << std::endl;
        std::cout << "Wrong guesses: ";
        for (char c : wrongGuesses) {
            std::cout << c << ' ';
        }
        std::cout << std::endl;
        std::cout << "Attempts left: " << maxAttempts - wrongGuesses.size() << std::endl;
    }

    bool makeGuess(char guess) {
        guess = tolower(guess);
        if (std::find(wrongGuesses.begin(), wrongGuesses.end(), guess) != wrongGuesses.end() ||
            std::find(guessedWord.begin(), guessedWord.end(), guess) != guessedWord.end()) {
            std::cout << "You've already guessed that letter!" << std::endl;
            return false;
        }

        bool correct = false;
        for (size_t i = 0; i < secretWord.size(); ++i) {
            if (secretWord[i] == guess) {
                guessedWord[i] = guess;
                correct = true;
            }
        }

        if (!correct) {
            wrongGuesses.push_back(guess);
        }

        return correct;
    }

    bool isGameOver() const {
        return guessedWord == secretWord || wrongGuesses.size() >= maxAttempts;
    }

    bool isGameWon() const {
        return guessedWord == secretWord;
    }

    void play() {
        while (!isGameOver()) {
            displayStatus();
            std::cout << "Enter your guess: ";
            char guess;
            std::cin >> guess;
            makeGuess(guess);
        }

        displayStatus();
        if (isGameWon()) {
            std::cout << "Congratulations! You've guessed the word: " << secretWord << std::endl;
        } else {
            std::cout << "Game over! The word was: " << secretWord << std::endl;
        }
    }
};

int main() {
    HangmanGame game;
    game.play();
    return 0;
}
