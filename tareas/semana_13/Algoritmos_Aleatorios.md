
# 🧮 Algoritmos Aleatorios y su Comportamiento

## ⏱️ ¿Qué es el Tiempo Esperado?

En los algoritmos que incorporan elementos aleatorios, el tiempo de ejecución no es constante, incluso cuando se usa la misma entrada de datos.  
Por esta razón, en lugar de evaluar un tiempo fijo o hacer un promedio sobre múltiples entradas, se considera el **tiempo esperado**, que representa un valor medio basado en múltiples ejecuciones del mismo algoritmo.

---

## 🆚 Comparativa: Enfoques de Medición en Algoritmos

| Aspecto Evaluado       | Enfoque Promedio                        | Enfoque de Tiempo Esperado                     |
|------------------------|-----------------------------------------|------------------------------------------------|
| Naturaleza del algoritmo | Funciona siempre igual (determinista)   | Incluye decisiones aleatorias (probabilista)   |
| ¿Qué cambia?           | La variación está en los datos de entrada | La variación ocurre dentro del algoritmo       |
| Cómo se mide el tiempo | Promedio calculado sobre múltiples entradas | Promedio de varias ejecuciones con la misma entrada |
| Tipo de entrada        | Cada ejecución puede tener una entrada diferente | La entrada permanece constante                |
| Objetivo del análisis  | Obtener una visión global del rendimiento | Entender el efecto del azar en la ejecución    |

---

## 🧪 Ejemplo ilustrativo

> Imagina un escenario donde un personaje puede elegir entre una solución rápida (pero costosa) o esperar por una solución gratuita.  
> El algoritmo evalúa los posibles resultados según el beneficio o costo **esperado** si se elige aleatoriamente.

Este análisis permite entender **cuánto se ganaría o perdería en promedio** según las decisiones aleatorias realizadas.

---

## 🔢 Uso de Números Aleatorios en Algoritmos

En algoritmos con comportamiento no determinista se emplean **valores aleatorios o pseudoaleatorios**, que permiten modelar fenómenos inciertos o procesos aleatorizados.

---

## ❓ ¿Qué son los Números Pseudoaleatorios?

Son secuencias numéricas generadas por algoritmos que siguen reglas fijas pero simulan comportamientos impredecibles.  
Aunque son calculados mediante fórmulas matemáticas, **su apariencia estadística es similar a la de valores realmente aleatorios**.

---

## 🧮 Generador Lineal Congruencial

Este es uno de los mecanismos más comunes para crear números pseudoaleatorios.  
Utiliza la siguiente fórmula matemática:

```
Xₙ₊₁ = (a * Xₙ + c) mod m
```

- `Xₙ`: valor actual o semilla inicial
- `a`, `c`, `m`: constantes cuidadosamente elegidas para asegurar una buena distribución

---

## 🛠️ ¿Dónde se usa este generador?

Este tipo de algoritmos tiene aplicaciones en muchas áreas, como:

- Modelado y simulación de sistemas
- Desarrollo de videojuegos
- Métodos de Monte Carlo
- Pruebas estadísticas
- Algoritmos con decisiones estocásticas


# Taller - Tarea en Casa.
-------------------------------------------------------------------------

<img width="1087" height="896" alt="image" src="https://github.com/user-attachments/assets/7b430281-6edd-4085-9e28-cd3a911428f4" />

-------------------------------------------------------------------------
### Código en Java:

```java
public class GeneradorCongruencialLineal {

    // Parámetros definidos
    private static final long a = 1664525;
    private static final long c = 1013904223;
    private static final long m = (long) Math.pow(2, 32); // 2^32

    private long semilla;

    // Constructor
    public GeneradorCongruencialLineal(long semillaInicial) {
        this.semilla = semillaInicial;
    }

    // Genera el siguiente número pseudoaleatorio
    public double siguienteNumero() {
        semilla = (a * semilla + c) % m;
        return (double) semilla / m; // normalizado a [0,1)
    }

    public static void main(String[] args) {
        long semillaInicial = 123456789; // Puedes cambiar la semilla

        GeneradorCongruencialLineal generador = new GeneradorCongruencialLineal(semillaInicial);

        // Generar 100 números pseudoaleatorios normalizados
        double[] numeros = new double[100];
        for (int i = 0; i < 100; i++) {
            numeros[i] = generador.siguienteNumero();
        }

        // Mostrar los primeros 10 valores generados
        System.out.println("Primeros 10 números generados:");
        for (int i = 0; i < 10; i++) {
            System.out.printf("número[%d] = %.10f%n", i + 1, numeros[i]);
        }
    }
}


```
### Resultado de la terminal.
<img width="1147" height="839" alt="image" src="https://github.com/user-attachments/assets/930ab0db-cbd3-403d-ac40-206d16e53820" />

# Taller - Número 2.
-------------------------------------------------------------------------

<img width="1047" height="904" alt="image" src="https://github.com/user-attachments/assets/99b48f72-aae6-42c0-8414-025002b6b119" />

-------------------------------------------------------------------------
### Código en Java:
```java
public class DistribucionGeneradorLineal {

    // Parámetros del generador lineal
    private static final long a = 1664525;
    private static final long c = 1013904223;
    private static final long m = (long) Math.pow(2, 32);

    private long semilla;

    public DistribucionGeneradorLineal(long semilla) {
        this.semilla = semilla;
    }

    // Genera un número pseudoaleatorio normalizado
    public double siguienteNumero() {
        semilla = (a * semilla + c) % m;
        return (double) semilla / m;
    }

    public static void main(String[] args) {
        long semillaInicial = 123456789L;
        DistribucionGeneradorLineal generador = new DistribucionGeneradorLineal(semillaInicial);

        int[] intervalos = new int[5]; // Contadores para los 5 intervalos
        double[] numeros = new double[100];

        for (int i = 0; i < 100; i++) {
            double num = generador.siguienteNumero();
            numeros[i] = num;

            // Contar en qué intervalo cae el número
            if (num < 0.2) intervalos[0]++;
            else if (num < 0.4) intervalos[1]++;
            else if (num < 0.6) intervalos[2]++;
            else if (num < 0.8) intervalos[3]++;
            else intervalos[4]++;
        }

        // Mostrar primeros 10 números
        System.out.println("Primeros 10 números generados:");
        for (int i = 0; i < 10; i++) {
            System.out.printf("número[%d] = %.10f%n", i + 1, numeros[i]);
        }

        // Mostrar distribución
        System.out.println("\nDistribución por intervalos:");
        System.out.printf("[0.0, 0.2): %d%n", intervalos[0]);
        System.out.printf("[0.2, 0.4): %d%n", intervalos[1]);
        System.out.printf("[0.4, 0.6): %d%n", intervalos[2]);
        System.out.printf("[0.6, 0.8): %d%n", intervalos[3]);
        System.out.printf("[0.8, 1.0): %d%n", intervalos[4]);

    }
}
```
### Resultado de la terminal.
<img width="902" height="984" alt="image" src="https://github.com/user-attachments/assets/b1744ea1-0e1f-4095-ae5a-fd4fc1d3faeb" />

## ✅ Respuestas al análisis

### 🌐 ¿La distribución es aproximadamente uniforme?

**Sí, es razonablemente uniforme.**

Distribución de los 100 números generados en los intervalos especificados:

| Intervalo      | Frecuencia |
|----------------|------------|
| [0.0, 0.2)     | 19         |
| [0.2, 0.4)     | 25         |
| [0.4, 0.6)     | 27         |
| [0.6, 0.8)     | 15         |
| [0.8, 1.0)     | 14         |

Aunque hay pequeñas diferencias entre intervalos, los valores están bastante equilibrados.  
Esto es normal en secuencias pseudoaleatorias y sugiere que el generador produce una **distribución aproximadamente uniforme**.

---

### 🔁 ¿Qué efecto tiene cambiar la semilla?

**Cambiar la semilla altera completamente la secuencia generada.**

- El generador congruencial lineal es **determinista**: si usas la misma semilla, obtendrás siempre la misma secuencia.
- Al cambiar la semilla, se produce una secuencia **diferente**, pero con características estadísticas similares (si el generador es bueno).
- Esto permite reproducibilidad (cuando se fija la semilla) o variabilidad (cuando se cambia).

---

