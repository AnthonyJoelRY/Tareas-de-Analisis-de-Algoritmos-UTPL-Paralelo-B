## Resultados de la ejecución:
![Imagen de WhatsApp 2025-06-07 a las 10 35 13_7ee6f2b2](https://github.com/user-attachments/assets/0b4827b3-844d-4c73-a3ee-9669b2ce3153)
## Codigo en java.(Kruskal)
```java
package algoritmokruskal;

import java.util.*;

public class Kruskal {

    static class Arista implements Comparable<Arista> {
        int origen, destino;
        Arista(int origen, int destino) {
            this.origen = origen;
            this.destino = destino;
        }

        @Override
        public int compareTo(Arista otra) {
            return 0; // no se ordena por peso porque ya están ordenadas manualmente
        }

        @Override
        public String toString() {
            return "(" + (origen + 1) + "," + (destino + 1) + ")";
        }
    }

    static class UnionFind {
        int[] padre;

        UnionFind(int n) {
            padre = new int[n];
            for (int i = 0; i < n; i++) padre[i] = i;
        }

        int buscar(int x) {
            if (padre[x] != x) padre[x] = buscar(padre[x]);
            return padre[x];
        }

        void unir(int a, int b) {
            int ra = buscar(a);
            int rb = buscar(b);
            if (ra != rb) padre[rb] = ra;
        }

        Map<Integer, List<Integer>> obtenerConjuntos() {
            Map<Integer, List<Integer>> conjuntos = new TreeMap<>();
            for (int i = 0; i < padre.length; i++) {
                int raiz = buscar(i);
                conjuntos.putIfAbsent(raiz, new ArrayList<>());
                conjuntos.get(raiz).add(i + 1); // +1 para que coincida con la imagen
            }
            return conjuntos;
        }
    }

    public static void main(String[] args) {
        int n = 7; // nodos 1 a 7
        List<Arista> aristas = Arrays.asList(
            new Arista(0, 1), // (1,2)
            new Arista(1, 2), // (2,3)
            new Arista(3, 4), // (4,5)
            new Arista(5, 6), // (6,7)
            new Arista(0, 3), // (1,4)
            new Arista(1, 4), // (2,5)
            new Arista(3, 6), // (4,7)
            new Arista(2, 4), // (3,5)
            new Arista(1, 3), // (2,4)
            new Arista(2, 5), // (3,6)
            new Arista(4, 6), // (5,7)
            new Arista(4, 5)  // (5,6)
        );

        UnionFind uf = new UnionFind(n);
        List<Arista> T = new ArrayList<>();

        System.out.println("Paso a paso del algoritmo de Kruskal:\n");

        for (Arista arista : aristas) {
            int compu = uf.buscar(arista.origen);
            int compv = uf.buscar(arista.destino);

            System.out.println("Arista considerada: " + arista);
            if (compu != compv) {
                System.out.println(" -> Se agregara al MST");
                T.add(arista);
                uf.unir(compu, compv);
            } else {
                System.out.println(" -> Se descarta (formaria ciclo)");
            }

            // Mostrar conjuntos actuales
            System.out.print(" Conjuntos: ");
            uf.obtenerConjuntos().values().forEach(conj -> System.out.print(conj + " "));
            System.out.println("\n MST hasta ahora: " + T + "\n");

            if (T.size() == n - 1) break;
        }

        System.out.println("Arbol de Recubrimiento Minimo final:");
        System.out.println(T);
    }
}
```
## Nota: 
#### El código fuente ejecutable se encuentra dentro del archivo .rar incluido en este repositorio.Además, la explicación detallada del algoritmo de Kruskal, junto con los resúmenes semanales, están disponibles en la sección Wiki del proyecto.
