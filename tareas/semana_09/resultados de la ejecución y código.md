## Algoritmo de Kruskal

El algoritmo de Kruskal permite construir un Árbol de Recubrimiento Mínimo (MST) a partir de un grafo no dirigido. Funciona agregando aristas en orden, evitando ciclos, hasta conectar todos los nodos.

### Implementación

En este proyecto se implementó Kruskal en Java, usando conjuntos disjuntos (Union-Find) para controlar los ciclos. Las aristas se agregan manualmente en el orden dado según el ejemplo visto en clase (nodos 1 al 7).

El programa muestra paso a paso:
- Qué arista se evalúa
- Si se agrega o se descarta
- El estado actual de los conjuntos
- El MST parcial

### Recursos
```java
package kruskall;
import java.util.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;

public class Kruskall {

    static class Arista implements Comparable<Arista> {
        int origen, destino, peso;

        public Arista(int origen, int destino, int peso) {
            this.origen = origen;
            this.destino = destino;
            this.peso = peso;
        }

        @Override
        public int compareTo(Arista otra) {
            return this.peso - otra.peso;
        }

        @Override
        public String toString() {
            return String.format("(%d - %d : %d)", origen, destino, peso);
        }
    }

    static class UnionFind {
        int[] padre, rango;

        public UnionFind(int n) {
            padre = new int[n];
            rango = new int[n];
            for (int i = 0; i < n; i++) {
                padre[i] = i;
                rango[i] = 0;
            }
        }

        public int encontrar(int u) {
            if (padre[u] != u)
                padre[u] = encontrar(padre[u]);
            return padre[u];
        }

        public boolean unir(int u, int v) {
            int raizU = encontrar(u);
            int raizV = encontrar(v);

            if (raizU == raizV) return false;

            if (rango[raizU] < rango[raizV]) {
                padre[raizU] = raizV;
            } else if (rango[raizU] > rango[raizV]) {
                padre[raizV] = raizU;
            } else {
                padre[raizV] = raizU;
                rango[raizU]++;
            }
            return true;
        }
    }

    public static void kruskal(int V, List<Arista> aristas) {
        Collections.sort(aristas);
        UnionFind uf = new UnionFind(V);
        List<Arista> mst = new ArrayList<>();
        int costoTotal = 0;

        System.out.println("\n--- Ejecucion paso a paso (prueba de escritorio) ---");
        for (Arista a : aristas) {
            System.out.printf("Considerando arista %s\n", a);
            if (uf.unir(a.origen, a.destino)) {
                mst.add(a);
                costoTotal += a.peso;
                System.out.println("  Incorporada al arbol");
            } else {
                System.out.println("  Se descarta (formaria un ciclo)");
            }
        }

        System.out.println("\nArbol de Recubrimiento Minimo:");
        for (Arista a : mst)
            System.out.println("  " + a);
        System.out.println("Costo total: " + costoTotal);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Ingrese el numero de vertices: ");
        int V = scanner.nextInt();

        System.out.print("Ingrese el numero de aristas: ");
        int E = scanner.nextInt();

        List<Arista> aristas = new ArrayList<>();

        System.out.println("Ingrese las aristas (formato: origen destino peso):");
        for (int i = 0; i < E; i++) {
            int u, v, peso;
            while (true) {
                System.out.printf("Arista %d: ", i + 1);
                u = scanner.nextInt();
                v = scanner.nextInt();
                peso = scanner.nextInt();

                if (u >= 0 && u < V && v >= 0 && v < V) {
                    break;
                } else {
                    System.out.println("Error: los vertices deben estar entre 0 y " + (V - 1) + ". Intente de nuevo.");
                }
            }
            aristas.add(new Arista(u, v, peso));
        }

        kruskal(V, aristas);
    }
}
```
### Ejecución:
<img width="660" height="992" alt="image" src="https://github.com/user-attachments/assets/38ca2fa5-3242-41f8-af9a-b1f1082ed9cb" />

### Trabajo en Clases.
![Imagen de WhatsApp 2025-07-20 a las 14 09 47_95fc6854](https://github.com/user-attachments/assets/cbae3615-ea4e-43b4-81ac-8d39928ddaf5)
![Imagen de WhatsApp 2025-07-20 a las 14 09 47_a9c2ba1e](https://github.com/user-attachments/assets/34f20ba5-819d-4356-8a26-cb4418e9346f)
