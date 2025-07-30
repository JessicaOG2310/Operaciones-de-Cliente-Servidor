# Operaciones-de-Cliente-Servidor
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.IOException;
import java.net.Socket;
import java.util.Scanner;

public class ClienteSuma {
    static Scanner lector = new Scanner(System.in);

    public ClienteSuma() {
        System.out.println("Cliente corriendo");
        try {
            Socket sc = new Socket("localhost", 5050);
            DataInputStream dis = new DataInputStream(sc.getInputStream());
            DataOutputStream dos = new DataOutputStream(sc.getOutputStream());

            int opcion;
            do {
                System.out.println(dis.readUTF()); // Elija la operacion que desea realizar:
                System.out.println(dis.readUTF()); // 1. Suma de numeros
                System.out.println(dis.readUTF()); // 2. Seno de un numero
                System.out.println(dis.readUTF()); // 3. Coseno de un numero
                System.out.println(dis.readUTF()); // 4. Raiz cuadrada de un numero
                System.out.println(dis.readUTF()); // 5. Elevar una base a una potencia
                System.out.println(dis.readUTF()); // 6. Salir del programa

                System.out.print("Ingrese su opcion: ");
                opcion = lector.nextInt();
                dos.writeInt(opcion);
                dos.flush();

                switch (opcion) {
                    case 1:
                        System.out.println(dis.readUTF()); // ¿Cuantos numeros desea enviar para que se sumen?
                        int cantidad = lector.nextInt();
                        dos.writeInt(cantidad);
                        dos.flush();
                        for (int i = 0; i < cantidad; i++) {
                            System.out.println(dis.readUTF()); // Ingrese un numero:
                            double num = lector.nextDouble();
                            dos.writeDouble(num);
                            dos.flush();
                        }
                        System.out.println(dis.readUTF()); // La suma es:
                        break;
                    case 2:
                        System.out.println(dis.readUTF()); // Ingresa el valor del angulo en grados:
                        double grados = lector.nextDouble();
                        dos.writeDouble(grados);
                        dos.flush();
                        System.out.println(dis.readUTF()); // Seno:
                        break;
                    case 3:
                        System.out.println(dis.readUTF()); // Ingresa el valor del angulo en grados:
                        double gradoss = lector.nextDouble();
                        dos.writeDouble(gradoss);
                        dos.flush();
                        System.out.println(dis.readUTF()); // Coseno:
                        break;
                    case 4:
                        System.out.println(dis.readUTF()); // Ingrese un numero:
                        int numRaiz = lector.nextInt();
                        dos.writeInt(numRaiz);
                        dos.flush();
                        System.out.println(dis.readUTF()); // Raiz cuadrada 
                        break;
                    case 5:
                        System.out.println(dis.readUTF()); // Escriba el numero que sera la base:
                        double base = lector.nextDouble();
                        dos.writeDouble(base);
                        dos.flush();
                        System.out.println(dis.readUTF()); // Escriba a que potencia sera elevada:
                        double potencia = lector.nextDouble();
                        dos.writeDouble(potencia);
                        dos.flush();
                        System.out.println(dis.readUTF()); // El resultado es:
                        break;
                    default:
                        System.out.println(dis.readUTF()); // Opcion invalida
                        break;
                }
            } while (opcion != 6);

            sc.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        new ClienteSuma();
    }
}
