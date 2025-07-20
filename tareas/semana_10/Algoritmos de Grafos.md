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
### Trabajo en Clases:
![Imagen de WhatsApp 2025-07-20 a las 10 20 27_67362bf4](https://github.com/user-attachments/assets/fd1b431a-1b25-4d30-a498-84cb9ccb8864)

🧾 **Resumen elaborado por**: Anthony Joel Romero Yaguana  
📅 **Fecha de actualización**: 21/06/2025  
🎓 **Materia**: Análisis de Algoritmos - UTPL
