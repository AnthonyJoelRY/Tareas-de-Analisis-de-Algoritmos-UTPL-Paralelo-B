
# 📊 ¿Qué es la Mediana y cómo se calcula?

La **mediana** es un valor estadístico que representa el punto medio de un conjunto de datos que han sido **ordenados previamente**.  
- Si la cantidad de datos es impar, la mediana corresponde al elemento ubicado justo en el centro.  
- Si el número de datos es par, se suele calcular el promedio entre los dos valores centrales, aunque en algunos contextos puede seleccionarse uno de ellos según criterios particulares.

---

## 🔎 Pasos para hallar la mediana

1. Ordena todos los elementos de menor a mayor.
2. Determina el valor central:
   - Si `n` (el número total de elementos) es impar → mediana = elemento en la posición `(n + 1) / 2`
   - Si `n` es par → mediana = promedio entre los dos valores centrales o se escoge uno según convenga al problema

Este proceso es sencillo, pero puede volverse costoso en tiempo si el conjunto de datos es muy grande y se requiere ordenarlo completamente.

---

## ⚙️ Aplicaciones prácticas en algoritmos

El cálculo de la mediana no solo es útil en estadística, también tiene un papel clave en la computación y el diseño de algoritmos:

- Es usada para dividir conjuntos de datos en partes iguales o balanceadas.
- Ayuda a establecer puntos de referencia en algoritmos de ordenamiento y búsqueda.
- Optimiza el desempeño de algoritmos como **Quickselect** o **Quicksort**, donde la mediana puede actuar como pivote para particionar datos eficientemente.

---

## 🧠 Algoritmos eficientes: divide y vencerás

En situaciones avanzadas, existen algoritmos que permiten hallar la mediana **sin necesidad de ordenar completamente** el conjunto.  
Estos algoritmos dividen los datos en subconjuntos, realizan comparaciones estratégicas y reducen el problema paso a paso.  
Este enfoque mejora significativamente la eficiencia, especialmente en grandes volúmenes de datos.

---

# ✖️ Multiplicación de Matrices: Conceptos Clave

La multiplicación de matrices es una operación fundamental en ciencias de la computación, álgebra lineal y modelado matemático.  
Consiste en combinar dos matrices (`A` y `B`) para obtener una nueva matriz resultado (`C`), siguiendo reglas específicas de compatibilidad.

---

## 📐 Regla general de multiplicación

Para que la operación sea válida:

- La matriz `A` debe tener tamaño `m x n`
- La matriz `B` debe tener tamaño `n x p`
- El resultado `C` será una matriz de tamaño `m x p`

Cada elemento `C[i][j]` se calcula aplicando la siguiente fórmula:

```math
C[i][j] = ∑ A[i][k] × B[k][j],  donde k va desde 1 hasta n
```

Es decir, se multiplica fila de `A` por columna de `B` y se suman los productos.

---

## 🧾 Ejemplo de multiplicación paso a paso

Supongamos que tenemos las siguientes matrices:

```text
A = [ [a11, a12],
      [a21, a22] ]

B = [ [b11, b12],
      [b21, b22] ]
```

La matriz `C` resultado de multiplicar `A × B` es:

```text
C[1][1] = a11 * b11 + a12 * b21
C[1][2] = a11 * b12 + a12 * b22
C[2][1] = a21 * b11 + a22 * b21
C[2][2] = a21 * b12 + a22 * b22
```

Este procedimiento puede extenderse fácilmente a matrices de cualquier dimensión compatible.

---

> 🧠 **Nota final:** Tanto el cálculo de la mediana como la multiplicación de matrices son herramientas básicas, pero extremadamente poderosas, cuando se dominan e integran en algoritmos más complejos.

### Trabajo en Clases:
https://utpl-my.sharepoint.com/:x:/g/personal/ajromero12_utpl_edu_ec/EVQwbsJVddhMlcjD7KgF_igBfxs18fqwjbTYb0DOmU1bkQ?e=XVLHCg
