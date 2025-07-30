import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.ArrayList;
import java.util.Scanner;

public class ServidorSuma {
    private ArrayList<Double> Numeros = new ArrayList<>();
    static Scanner lector = new Scanner(System.in);

    public ServidorSuma() throws IOException {
        ServerSocket ss = new ServerSocket(5050);
        Socket s = ss.accept();
        DataInputStream dis = new DataInputStream(s.getInputStream());
        DataOutputStream dos = new DataOutputStream(s.getOutputStream());

        System.out.println("Servidor iniciado");
        int opcion;
        do {
            dos.writeUTF("Elija la operacion que desea realizar:");
            dos.writeUTF("1. Suma de numeros");
            dos.writeUTF("2. Seno de un numero");
            dos.writeUTF("3. Coseno de un numero");
            dos.writeUTF("4. Raiz cuadrada de un numero");
            dos.writeUTF("5. Elevar una base a una potencia");
            dos.writeUTF("6. Salir del programa");
            dos.flush();

            opcion = dis.readInt();

            switch (opcion) {
                case 1:
                    dos.writeUTF("¿Cuantos numeros desea enviar para que se sumen?");
                    dos.flush();
                    int cantidad = dis.readInt();
                    double suma = 0;
                    for (int i = 0; i < cantidad; i++) {
                        dos.writeUTF("Ingrese un numero: ");
                        dos.flush();
                        double num = dis.readDouble();
                        Numeros.add(num);
                        suma += num;
                    }
                    dos.writeUTF("La suma es: " + suma);
                    dos.flush();
                    Numeros.clear();
                    break;
                case 2:
                    dos.writeUTF("Ingresa el valor del angulo en grados: ");
                    dos.flush();
                    double grados = dis.readDouble();
                    double radianes = grados * Math.PI / 180;
                    double seno = Math.sin(radianes);
                    dos.writeUTF("Seno: " + seno);
                    dos.flush();
                    break;
                case 3:
                    dos.writeUTF("Ingresa el valor del angulo en grados: ");
                    dos.flush();
                    double gradoss = dis.readDouble();
                    double radianess = gradoss * Math.PI / 180;
                    double coseno = Math.cos(radianess);
                    dos.writeUTF("Coseno: " + coseno);
                    dos.flush();
                    break;
                case 4:
                    dos.writeUTF("Ingrese un numero: ");
                    dos.flush();
                    int numRaiz = dis.readInt();
                    double raiz = Math.sqrt(numRaiz);
                    dos.writeUTF("Raiz cuadrada del " + numRaiz + " es: " + raiz);
                    dos.flush();
                    break;
                case 5:
                    dos.writeUTF("Escriba el numero que sera la base: ");
                    dos.flush();
                    double base = dis.readDouble();
                    dos.writeUTF("Escriba a que potencia sera elevada: ");
                    dos.flush();
                    double potencia = dis.readDouble();
                    double resultado = Math.pow(base, potencia);
                    dos.writeUTF("El resultado es: " + resultado);
                    dos.flush();
                    break;
                default:
                    dos.writeUTF("Opcion invalida");
                    dos.flush();
                    break;
            }
        } while (opcion != 6);

        ss.close();
        s.close();
    }

    public static void main(String[] args) {
        try {
            new ServidorSuma();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
