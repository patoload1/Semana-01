| <div align="right"><img src="Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Sesión 1 (Estudiantes)

**Duración:** 2 horas  
**Tema:** Relaciones – repaso y Upcast

---

## Explicación (resumen)

- **Relaciones entre clases:** Generalización (herencia), dependencia y asociación (agregación/composición). Distinga "es-un" de "tiene-un".
- **Upcast:** Conversión de puntero o referencia de clase derivada a clase base. Es segura e implícita; permite polimorfismo.

---

## Espacio para tu código

Escriba su implementación en los bloques siguientes. El profesor validará que esté bien escrito.

### Ejercicio 1: Vehiculo y Automovil – upcast

Defina `Vehiculo` (base) y `Automovil` (derivada). En `main` cree un `Automovil` y asígnelo a un puntero (o referencia) a `Vehiculo`. Justifique en comentarios por qué es upcast y es seguro.

```cpp
#include <iostream>
using namespace std;

// Escriba aquí la clase Vehiculo


// Escriba aquí la clase Automovil


int main() {
    // Escriba aquí: crear Automovil y upcast a Vehiculo*


    return 0;
}
```

### Ejercicio 2: Jerarquía de 3 niveles

Escriba una jerarquía base → derivada1 → derivada2. En `main` realice upcast en cada nivel a la clase base y llame un método definido en la base.

```cpp
// Escriba aquí las tres clases y main con upcast

```

### Ejercicio 3: Array de punteros a base

Defina una clase base abstracta `Figura` (con `double area() = 0`) y derive `Circulo` y `Rectangulo`. En `main` use un **array** de punteros `Figura* figuras[MAX]`, agregue figuras y recorra el array mostrando el área. No use `vector`.

```cpp
// Escriba aquí: Figura, Circulo, Rectangulo y main con array Figura* figuras[MAX]

```

---

## Criterios de validación (para el profesor)

- [ ] Uso de `using namespace std;`
- [ ] Upcast correcto (puntero/referencia derivada → base)
- [ ] Uso de **array** de punteros (no vector) en el ejercicio 3
- [ ] Constructores sin sintaxis `b(base), h(alt)`; usar asignación en el cuerpo si aplica
