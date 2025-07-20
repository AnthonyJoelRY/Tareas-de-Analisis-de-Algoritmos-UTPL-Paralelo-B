# 📚 Divide y Vencerás & Búsqueda Binaria — UTPL

## Introducción

El paradigma **Divide y Vencerás** consiste en descomponer un problema complejo en subproblemas más simples, resolverlos individualmente y luego combinar las soluciones. Este enfoque es fundamental en algoritmos eficientes como la búsqueda binaria y la multiplicación rápida.

---

## ⚙️ Divide y Vencerás

Una aplicación matemática del enfoque:

```
981 × 1234 = (10²w + x)(10²y + z)
           = 10⁴wy + 10²(wz + xy) + xz
```

La expresión puede reescribirse usando un solo producto:

```
r = (w + x)(y + z) = wy + (wz + xy) + xz
```

👉 Esto es útil para algoritmos de multiplicación como **Karatsuba**, que minimizan el número de operaciones.

---

## 🔍 Búsqueda Secuencial

```java
public static int Secuencial(int[] T, int x) {
    int Encontrado = -1;
    int i = 0;
    while (Encontrado == -1 && i < T.length) {
        if (T[i] == x)
            Encontrado = i;
        i++;
    }
    return Encontrado;
}
```

### ⏱️ Complejidad:
- **Peor caso**: Θ(n)
- **Mejor caso**: Θ(1)

---

## 🔎 Búsqueda Binaria Recursiva

```java
public static int BinRec(int[] T, int i, int j, int x) {
    if (i == j) return i;
    int k = (i + j) / 2;
    if (x <= T[k])
        return BinRec(T, i, k, x);
    else
        return BinRec(T, k + 1, j, x);
}

public static int BusquedaBin(int[] T, int x) {
    int n = T.length;
    if (n == 0 || x > T[n - 1]) return n + 1;
    return BinRec(T, 0, n, x);
}
```

---

## 🔁 Búsqueda Binaria Iterativa

```java
public static int BinIter(int[] T, int x) {
    int n = T.length;
    if (x > T[n - 1]) return n + 1;
    int i = 0, j = n;
    while (i < j) {
        int k = (i + j) / 2;
        if (x <= T[k])
            j = k;
        else
            i = k + 1;
    }
    return i;
}
```

### ⏱️ Complejidad:
- **Mejor caso**: Θ(1)
- **Peor caso**: Θ(log n)
- **Promedio**: Θ(log(n/2))

---

## 🧪 Prueba de Escritorio

Arreglo de prueba:
```
8, 10, 14, 24, 28, 35, 49, 56, 98
```

Se utiliza para trazar el recorrido del algoritmo y verificar su exactitud paso a paso.

---

## ✅ Conclusión

La búsqueda binaria demuestra cómo el paradigma *divide y vencerás* puede optimizar procesos, reduciendo el tiempo de ejecución de **Θ(n)** a **Θ(log n)**. Esta eficiencia la convierte en un recurso fundamental en estructuras ordenadas.

---
### Trabajo en Clases:
https://utpl-my.sharepoint.com/:x:/g/personal/ajromero12_utpl_edu_ec/EZtcV-N6yCxPsmodZMAkqQABy3na_ATSQ_UkZrrhFoEizA?e=B7YZdb

📘 _Curso: Análisis de Algoritmos - UTPL_  
📅 _Fecha: 16/06/2025_  
👨‍💻 _Alumno: Anthony Joel Romero Yaguana_
