#QUIZ APPLICATION 
import java.util.*;

class Question {
    String questionText;
    String[] options;
    int correctAnswerIndex;

    public Question(String questionText, String[] options, int correctAnswerIndex) {
        this.questionText = questionText;
        this.options = options;
        this.correctAnswerIndex = correctAnswerIndex;
    }
}

class Quiz {
    private List<Question> questions;
    private int score;

    public Quiz() {
        this.questions = new ArrayList<>();
        this.score = 0;
    }

    public void addQuestion(Question question) {
        questions.add(question);
    }

    public void startQuiz() {
        Scanner scanner = new Scanner(System.in);
        for (int i = 0; i < questions.size(); i++) {
            Question q = questions.get(i);
            displayQuestion(q, i + 1);

            long startTime = System.currentTimeMillis();
            int userAnswer = getUserAnswer(scanner);
            long elapsedTime = System.currentTimeMillis() - startTime;

            if (elapsedTime > 10000) {  // 10 seconds limit
                System.out.println("Time's up! No points for this question.");
            } else if (userAnswer == q.correctAnswerIndex + 1) {
                System.out.println("Correct!");
                score++;
            } else {
                System.out.println("Incorrect.");
            }

            System.out.println();
        }

        displayResults();
    }

    private void displayQuestion(Question question, int questionNumber) {
        System.out.println("Question " + questionNumber + ": " + question.questionText);
        for (int i = 0; i < question.options.length; i++) {
            System.out.println((i + 1) + ". " + question.options[i]);
        }
    }

    private int getUserAnswer(Scanner scanner) {
        System.out.print("Your answer: ");
        return scanner.nextInt();
    }

    private void displayResults() {
        System.out.println("Quiz finished!");
        System.out.println("Your final score: " + score + "/" + questions.size());
    }
}

public class QuizApp {
    public static void main(String[] args) {
        Quiz quiz = new Quiz();
        // Add questions
        quiz.addQuestion(new Question(
                "What is the capital of France?",
                new String[]{"Berlin", "London", "Paris", "Rome"},
                2
        ));
        quiz.addQuestion(new Question(
                "Which planet is known as the Red Planet?",
                new String[]{"Earth", "Mars", "Jupiter", "Venus"},
                1
        ));
        quiz.addQuestion(new Question(
                "Who wrote 'To Kill a Mockingbird'?",
                new String[]{"Harper Lee", "George Orwell", "J.K. Rowling", "Ernest Hemingway"},
                0
        ));

        // Start the quiz
        quiz.startQuiz();
    }
}
