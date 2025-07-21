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
### Ejecución:
<img width="660" height="992" alt="image" src="https://github.com/user-attachments/assets/38ca2fa5-3242-41f8-af9a-b1f1082ed9cb" />

### Trabajo en Clases.
![Imagen de WhatsApp 2025-07-20 a las 14 09 47_95fc6854](https://github.com/user-attachments/assets/cbae3615-ea4e-43b4-81ac-8d39928ddaf5)
![Imagen de WhatsApp 2025-07-20 a las 14 09 47_a9c2ba1e](https://github.com/user-attachments/assets/34f20ba5-819d-4356-8a26-cb4418e9346f)
