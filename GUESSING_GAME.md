# GUESSING GAME
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        int score = 0;
        boolean playAgain;

        do {
            int randomNumber = random.nextInt(100) + 1; // Generate a random number between 1 and 100
            int attempts = 0;
            boolean hasGuessedCorrectly = false;

            System.out.println("I have generated a random number between 1 and 100.");
            System.out.println("You have 10 attempts to guess the number.");

            while (attempts < 10 && !hasGuessedCorrectly) {
                System.out.print("Enter your guess: ");
                int userGuess = scanner.nextInt();
                attempts++;

                if (userGuess == randomNumber) {
                    System.out.println("Congratulations! You guessed the correct number.");
                    hasGuessedCorrectly = true;
                    score += 10 - attempts + 1; // Score is based on the number of attempts taken
                } else if (userGuess < randomNumber) {
                    System.out.println("Too low. Try again.");
                } else {
                    System.out.println("Too high. Try again.");
                }
            }

            if (!hasGuessedCorrectly) {
                System.out.println("Sorry, you've used all your attempts. The correct number was " + randomNumber);
            }

            System.out.print("Do you want to play again? (yes/no): ");
            playAgain = scanner.next().equalsIgnoreCase("yes");
        } while (playAgain);

        System.out.println("Your final score is: " + score);
        scanner.close();
    }
}
