
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
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.*;

public class KruskalGUI extends JFrame {

    private JTextArea outputArea;
    private JTextField verticesField, aristasField;
    private java.util.List<Kruskal.Arista> aristas = new ArrayList<>();
    private int vertices;

    public KruskalGUI() {
        setTitle("Arbol de Recubrimiento Minimo - Kruskal");
        setSize(550, 500);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        JPanel inputPanel = new JPanel(new GridLayout(3, 2));
        inputPanel.add(new JLabel("Numero de vertices:"));
        verticesField = new JTextField();
        inputPanel.add(verticesField);

        inputPanel.add(new JLabel("Numero de aristas:"));
        aristasField = new JTextField();
        inputPanel.add(aristasField);

        JButton iniciarBtn = new JButton("Ingresar Aristas");
        inputPanel.add(iniciarBtn);

        add(inputPanel, BorderLayout.NORTH);

        outputArea = new JTextArea();
        outputArea.setEditable(false);
        add(new JScrollPane(outputArea), BorderLayout.CENTER);

        iniciarBtn.addActionListener(e -> ingresarAristas());
    }

    private void ingresarAristas() {
        try {
            vertices = Integer.parseInt(verticesField.getText());
            int cantidadAristas = Integer.parseInt(aristasField.getText());
            aristas.clear();

            for (int i = 0; i < cantidadAristas; i++) {
                String entrada = JOptionPane.showInputDialog(this,
                        "Arista " + (i + 1) + " (formato: origen destino peso):");
                String[] partes = entrada.trim().split("\\s+");
                int u = Integer.parseInt(partes[0]);
                int v = Integer.parseInt(partes[1]);
                int peso = Integer.parseInt(partes[2]);

                if (u < 0 || u >= vertices || v < 0 || v >= vertices) {
                    JOptionPane.showMessageDialog(this, "Error: vertices fuera de rango (0 a " + (vertices - 1) + ")");
                    i--;
                    continue;
                }

                aristas.add(new Kruskal.Arista(u, v, peso));
            }

            ejecutarKruskal();

        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Por favor, ingrese solo numeros validos.");
        }
    }

    private void ejecutarKruskal() {
        outputArea.setText("");
        Collections.sort(aristas);
        Kruskal.UnionFind uf = new Kruskal.UnionFind(vertices);
        List<Kruskal.Arista> mst = new ArrayList<>();
        int costoTotal = 0;

        outputArea.append("--- Ejecucion paso a paso del algoritmo Kruskal ---\n");
        for (Kruskal.Arista a : aristas) {
            outputArea.append("Evaluando arista " + a + "\n");
            if (uf.unir(a.origen, a.destino)) {
                mst.add(a);
                costoTotal += a.peso;
                outputArea.append("  --> Agregada al arbol\n");
            } else {
                outputArea.append("  --> Descartada (formaria ciclo)\n");
            }
        }

        outputArea.append("\nResultado final del Arbol de Recubrimiento Minimo:\n");
        for (Kruskal.Arista a : mst)
            outputArea.append("  " + a + "\n");
        outputArea.append("Costo total: " + costoTotal + "\n");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new KruskalGUI().setVisible(true));
    }
}

class Kruskal {
    static class Arista implements Comparable<Arista> {
        int origen, destino, peso;

        public Arista(int origen, int destino, int peso) {
            this.origen = origen;
            this.destino = destino;
            this.peso = peso;
        }

        @Override
        public int compareTo(Arista otra) {
            return Integer.compare(this.peso, otra.peso);
        }

        @Override
        public String toString() {
            return "(" + origen + " - " + destino + " : " + peso + ")";
        }
    }

    static class UnionFind {
        int[] padre, rango;

        public UnionFind(int n) {
            padre = new int[n];
            rango = new int[n];
            for (int i = 0; i < n; i++) padre[i] = i;
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
}

```
### Resultado de la terminal de java:
<img width="660" height="992" alt="image" src="https://github.com/user-attachments/assets/38ca2fa5-3242-41f8-af9a-b1f1082ed9cb" />


