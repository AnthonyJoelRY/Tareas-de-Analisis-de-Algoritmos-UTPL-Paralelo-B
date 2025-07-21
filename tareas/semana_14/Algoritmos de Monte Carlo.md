
# 🎲 Introducción a los Algoritmos de Monte Carlo

Los **algoritmos de Monte Carlo** pertenecen a la categoría de algoritmos estocásticos, donde se utiliza el **azar como herramienta computacional**.  
Estos métodos no siempre entregan una respuesta exacta, pero ofrecen **resultados aproximados con un margen de error bajo y controlado**, especialmente útiles en contextos donde una solución determinista sería demasiado costosa o compleja.

---

## ⭐ Rasgos destacados

- **Alta eficiencia**: Ejecutan rápidamente tareas que serían lentas con enfoques clásicos.
- **Resultados variables**: La misma entrada puede producir diferentes salidas debido a su naturaleza aleatoria.
- **Tolerancia al error**: Existe una posibilidad de fallo, pero se minimiza repitiendo el proceso múltiples veces.
- **Confiabilidad estadística**: Aunque no son infalibles, sus respuestas tienden a ser correctas con alta probabilidad.

---

## 📛 ¿De dónde viene el nombre "Monte Carlo"?

El nombre se inspira en el famoso casino de Mónaco, ya que estos algoritmos **emulan juegos de azar** mediante el uso de números aleatorios o pseudoaleatorios.  
Fueron diseñados para abordar situaciones donde no es posible o no vale la pena encontrar una solución exacta, por lo que se usan simulaciones para tomar decisiones o estimar resultados.

---

## 🔍 Caso ilustrativo: Estimación de π

Uno de los ejemplos más comunes de aplicación es la estimación del valor de π:

1. Se generan puntos aleatorios dentro de un cuadrado.
2. Se determina cuántos caen dentro de un círculo inscrito.
3. Se calcula π con base en la proporción de puntos en el círculo respecto al total.

Este enfoque utiliza la **probabilidad geométrica** para aproximar un valor matemático.

---

## ✅ Beneficios

- Son eficaces cuando los algoritmos tradicionales resultan lentos o inviable su implementación.
- Ideales para procesos como simulación, integración, y problemas de optimización.
- Su precisión mejora a medida que se incrementa el número de ejecuciones o muestras.

---

## ⚠️ Consideraciones o limitaciones

- No garantizan una solución exacta, solo una estimación confiable.
- Requieren **validación estadística** para medir el nivel de confianza y precisión del resultado.
- La calidad del generador de números aleatorios utilizado impacta directamente en los resultados.

---

## 📌 Ámbitos donde se aplican

- Finanzas: modelado de riesgos e inversiones
- Ciencias físicas: simulación de partículas o fenómenos naturales
- Inteligencia artificial: toma de decisiones con incertidumbre
- Juegos y motores gráficos: generación de eventos o resultados aleatorios

### Tarea en Casa:
### Código en Java:
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
### Resultado de la terminal de java:
<img width="660" height="992" alt="image" src="https://github.com/user-attachments/assets/38ca2fa5-3242-41f8-af9a-b1f1082ed9cb" />


