import java.util.Random;
import java.util.Scanner;

public class CartaForbiciSasso {

    // variabili
    private int pUtente;
    private int pComputer;
    private int nPartite;

    // costrtuttore
    public CartaForbiciSasso() {
        pUtente = 0;
        pComputer = 0;
        nPartite = 0;
    }

    Scanner scanner = new Scanner(System.in);
    Random random = new Random();

    public void Gioca() {

        System.out.println("Benvenuto a Carta, Forbici, Sasso!");

        while (true) {
            System.out.println("Digita 'c' per CARTA, 'f' per FORBICI o 's' per SASSO");
            String sceltaUtente = scanner.nextLine().toUpperCase();

            if (sceltaUtente.equals("C") ||
                    sceltaUtente.equals("F") ||
                    sceltaUtente.equals("S")) {

                String[] scelta = { "C", "F", "S" };

                String sceltaComputer = scelta[random.nextInt(3)];

                System.out.println("Scelta computer: " + sceltaComputer);

                int risultatoRound = confrontaScelte(sceltaUtente, sceltaComputer);

                switch (risultatoRound) {
                    case 0:
                        System.out.println("Round pari!");
                        break;
                    case 1:
                        System.out.println("Round vinto dall' utente");
                        pUtente++;
                        break;
                    case -1:
                        System.out.println("Round vinto dal computer");
                        pComputer++;
                        break;
                }
                nPartite++;

                System.out.println("Punteggio - Utente: " + pUtente + " Computer: " + pComputer);

                // while = entra nel ciclo almeno una volta
                if (!(nPartite <= 2)) {

                    System.out.println("Fine round");
                    nPartite = 0;
                    System.out.print("Vuoi giocare ancora? (Sì/No): ");

                    String risposta = scanner.nextLine().toUpperCase();

                    if (risposta.equals("NO")) {
                        break;
                    }
                }
            } else {
                System.out.println("Scelta non valida. Riprova.");
            } // fine metodo
        } // fine while

        if (pUtente > pComputer) {
            System.out.println("Partita vinta dall' utente");
        } else if (pUtente < pComputer) {
            System.out.println("Partita vinta dal computer");
        } else {
            System.out.println("Partita pari");
        }
    }

    private int confrontaScelte(String utente, String computer) {
        switch (utente) {
            case "C":
                return computer.equals("S") ? 1 : computer.equals("F") ? -1 : 0;
            case "F":
                return computer.equals("C") ? 1 : computer.equals("S") ? -1 : 0;
            case "S":
                return computer.equals("F") ? 1 : computer.equals("C") ? -1 : 0;
            default:
                return 0;
        }
    }

    public static void main(String[] args) {
        CartaForbiciSasso gioco = new CartaForbiciSasso();
        gioco.Gioca();
    }
}
