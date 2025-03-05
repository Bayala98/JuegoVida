import java.util.Random;

public class Main {

    // Dimensiones de la matriz
    private static final int FILAS = 10;
    private static final int COLUMNAS = 10;

    // Método para imprimir la matriz
    public static void imprimirMatriz(char[][] matriz) {
        for (int i = 0; i < FILAS; i++) {
            for (int j = 0; j < COLUMNAS; j++) {
                System.out.print(matriz[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Método para inicializar la matriz aleatoriamente
    public static void inicializarMatriz(char[][] matriz) {
        Random rand = new Random();
        for (int i = 0; i < FILAS; i++) {
            for (int j = 0; j < COLUMNAS; j++) {
                matriz[i][j] = rand.nextBoolean() ? '*' : ' ';
            }
        }
    }

    // Método para contar los vecinos vivos de una célula
    public static int contarVecinosVivos(char[][] matriz, int fila, int columna) {
        int contador = 0;
        for (int i = fila - 1; i <= fila + 1; i++) {
            for (int j = columna - 1; j <= columna + 1; j++) {
                if (i >= 0 && i < FILAS && j >= 0 && j < COLUMNAS && (i != fila || j != columna)) {
                    if (matriz[i][j] == '*') {
                        contador++;
                    }
                }
            }
        }
        return contador;
    }

    // Método para aplicar las reglas del Juego de la Vida
    public static void siguienteGeneracion(char[][] matriz) {
        char[][] nuevaMatriz = new char[FILAS][COLUMNAS];

        for (int i = 0; i < FILAS; i++) {
            for (int j = 0; j < COLUMNAS; j++) {
                int vecinosVivos = contarVecinosVivos(matriz, i, j);
                if (matriz[i][j] == '*') {
                    if (vecinosVivos < 2 || vecinosVivos > 3) {
                        nuevaMatriz[i][j] = ' ';
                    } else {
                        nuevaMatriz[i][j] = '*';
                    }
                } else {
                    if (vecinosVivos == 3) {
                        nuevaMatriz[i][j] = '*';
                    } else {
                        nuevaMatriz[i][j] = ' ';
                    }
                }
            }
        }

        // Actualizamos la matriz original con la nueva generación
        for (int i = 0; i < FILAS; i++) {
            for (int j = 0; j < COLUMNAS; j++) {
                matriz[i][j] = nuevaMatriz[i][j];
            }
        }
    }

    public static void main(String[] args) {
        // Crear la matriz 10x10
        char[][] matriz = new char[FILAS][COLUMNAS];

        // Inicializar aleatoriamente
        inicializarMatriz(matriz);

        // Mostrar estado inicial
        System.out.println("Estado inicial:");
        imprimirMatriz(matriz);

        // Aplicar las reglas del juego para una nueva generación
        siguienteGeneracion(matriz);

        // Mostrar estado posterior
        System.out.println("\nEstado posterior:");
        imprimirMatriz(matriz);
    }
}
