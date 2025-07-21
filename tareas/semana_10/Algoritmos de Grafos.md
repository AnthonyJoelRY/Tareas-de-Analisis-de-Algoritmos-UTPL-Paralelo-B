# 🌐 Algoritmos de Grafos – UTPL

## 🧠 Algoritmo de Prim

El algoritmo de **Prim** se utiliza para encontrar el **árbol de expansión mínima** (MST) de un grafo no dirigido y conexo. Parte desde un nodo arbitrario y, en cada paso, agrega la arista de menor peso que conecta un nodo ya incluido con uno que no lo está.

### 📌 Características:
- Funciona sobre **grafos no dirigidos** con pesos en sus aristas.
- Utiliza estructuras como colas de prioridad o arreglos para seleccionar la arista mínima.
- Requiere que todas las aristas tengan **pesos no negativos**.

### 🧮 Pseudocódigo del Algoritmo:

```pseudo
Prim(G, nodo_inicio):
    Para cada vértice v en G:
        distancia[v] ← ∞
        padre[v] ← nulo
        visitado[v] ← falso

    distancia[nodo_inicio] ← 0

    Mientras existan vértices no visitados:
        u ← vértice no visitado con menor distancia[u]
        visitado[u] ← verdadero

        Para cada vecino v de u:
            si peso(u, v) < distancia[v] y v no visitado:
                distancia[v] ← peso(u, v)
                padre[v] ← u
```

---

## 🔁 Grafo Dirigido

Un **grafo dirigido** está compuesto por **arcos** (también llamados aristas dirigidas), donde el orden importa:

- Un **arco (v, w)** va del vértice `v` (cola) al vértice `w` (cabeza).
- Este arco representa una conexión **unidireccional**.

### 📦 Representaciones comunes:

1. **Listas enlazadas de adyacencia**  
   Cada nodo apunta a una lista de sus vecinos.

2. **Matriz de adyacencia (arreglo bidimensional)**  
   Una celda `[i][j]` contiene el **peso** de la arista de `i` a `j`, o `∞` si no existe.

### 🧾 Nota:
> El **peso** de cada arco es el valor almacenado en la estructura de datos. Este valor es crucial para los algoritmos que calculan rutas mínimas.

---

## 📍 Algoritmo de Dijkstra

> 📸 *Insertar Foto D del algoritmo*

El algoritmo de **Dijkstra** permite calcular el **camino más corto** desde un nodo origen a todos los demás nodos en un grafo con pesos no negativos.

### ⚙️ Funcionamiento:
1. Inicializa las distancias a todos los nodos como ∞, excepto al nodo origen (0).
2. Usa una **cola de prioridad** para seleccionar el nodo más cercano aún no visitado.
3. Relaja las aristas salientes del nodo seleccionado.
4. Repite hasta visitar todos los nodos.

### ✅ Requisitos:
- Grafo dirigido o no dirigido.
- Pesos **no negativos** en las aristas.

### 📈 Complejidad:
- Con cola de prioridad: **O((V + E) log V)** usando un heap binario.
### Tarea en Casa:
### Aplicación para determinar el camino mínimo a partir de un grafo dirigido
### Código:
```java
import java.util.*;

public class CaminoMinimoDijkstra {

    static class Arista {
        int destino;
        int peso;

        Arista(int destino, int peso) {
            this.destino = destino;
            this.peso = peso;
        }
    }

    public static void dijkstra(List<List<Arista>> grafo, int origen) {
        int n = grafo.size();
        int[] distancia = new int[n];
        Arrays.fill(distancia, Integer.MAX_VALUE);
        distancia[origen] = 0;

        PriorityQueue<int[]> cola = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        cola.add(new int[]{origen, 0});

        while (!cola.isEmpty()) {
            int[] actual = cola.poll();
            int nodo = actual[0];
            int dist = actual[1];

            if (dist > distancia[nodo]) continue;

            for (Arista arista : grafo.get(nodo)) {
                int nuevoDist = distancia[nodo] + arista.peso;
                if (nuevoDist < distancia[arista.destino]) {
                    distancia[arista.destino] = nuevoDist;
                    cola.add(new int[]{arista.destino, nuevoDist});
                }
            }
        }

        System.out.println("Distancias mínimas desde el nodo " + origen + ":");
        for (int i = 0; i < distancia.length; i++) {
            System.out.println("A nodo " + i + ": " + (distancia[i] == Integer.MAX_VALUE ? "Inalcanzable" : distancia[i]));
        }
    }

    public static void main(String[] args) {
        int nodos = 5; // número de nodos del grafo
        List<List<Arista>> grafo = new ArrayList<>();

        for (int i = 0; i < nodos; i++) {
            grafo.add(new ArrayList<>());
        }

        // Añadir aristas: grafo.get(origen).add(new Arista(destino, peso));
        grafo.get(0).add(new Arista(1, 10));
        grafo.get(0).add(new Arista(3, 5));
        grafo.get(1).add(new Arista(2, 1));
        grafo.get(1).add(new Arista(3, 2));
        grafo.get(2).add(new Arista(4, 4));
        grafo.get(3).add(new Arista(1, 3));
        grafo.get(3).add(new Arista(2, 9));
        grafo.get(3).add(new Arista(4, 2));
        grafo.get(4).add(new Arista(0, 7));
        grafo.get(4).add(new Arista(2, 6));

        int nodoOrigen = 0;
        dijkstra(grafo, nodoOrigen);
    }
}

```
### Ejecución:
<img width="1439" height="840" alt="image" src="https://github.com/user-attachments/assets/98e8c5cd-738a-4deb-99cd-15ec6d7fcde4" />

## Taller hecho en clase:
![Imagen de WhatsApp 2025-07-20 a las 10 20 27_3f07864f](https://github.com/user-attachments/assets/5403d365-bc26-4315-a3a2-2d6e827e0d28)

🧾 **Resumen elaborado por**: Anthony Joel Romero Yaguana  
📅 **Fecha de actualización**: 21/06/2025  
🎓 **Materia**: Análisis de Algoritmos - UTPL
