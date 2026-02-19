| <div align="right"><img src="../Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="../images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Sección general: Dependencia mutua (referencias circulares)

Material de apoyo para la Sesión 2.

---

## ¿Qué es?

Ocurre cuando:

- **Clase A** usa **B**
- **Clase B** usa **A**

**Ejemplo típico en el curso:**

- Estudiante → Curso  
- Curso → Estudiante  

Es decir:

- Un estudiante está inscrito en un curso.
- Un curso tiene estudiantes inscritos.

Lógicamente tiene sentido. **El problema no es conceptual, es de compilación.**

---

## El problema real (dependencia circular)

Supongamos estos archivos:

**Estudiante.h**

```cpp
#include "Curso.h"

class Estudiante {
private:
    Curso* curso;
};
```

**Curso.h**

```cpp
#include "Estudiante.h"

class Curso {
private:
    Estudiante* estudiante;
};
```

**¿Qué pasa?**

El compilador entra en un ciclo:

1. `Estudiante.h` necesita `Curso.h`
2. `Curso.h` necesita `Estudiante.h`
3. `Curso.h` vuelve a necesitar `Estudiante.h`
4. … y así sucesivamente.

Eso se llama **dependencia circular**.

---

## ¿Cómo se resuelve?

### Con forward declaration (declaración adelantada)

En lugar de incluir el header completo, declaramos que la clase existe:

```cpp
class Curso;   // forward declaration
```

Esto le dice al compilador:

*“Confía en mí, existe una clase llamada Curso. No necesitas saber todavía cómo está definida.”*

### Versión correcta

**Estudiante.h**

```cpp
#ifndef ESTUDIANTE_H
#define ESTUDIANTE_H

class Curso;   // forward declaration

class Estudiante {
private:
    Curso* curso;

public:
    void inscribir(Curso* c);
};

#endif
```

**Curso.h**

```cpp
#ifndef CURSO_H
#define CURSO_H

class Estudiante;   // forward declaration

class Curso {
private:
    Estudiante* estudiante;

public:
    void asignarEstudiante(Estudiante* e);
};

#endif
```

**Estudiante.cpp**  
Aquí sí incluimos el header completo:

```cpp
#include "Estudiante.h"
#include "Curso.h"

void Estudiante::inscribir(Curso* c) {
    curso = c;
}
```

---

## ¿Por qué esto funciona?

Porque estamos usando:

```cpp
Curso* curso;
```

Un **puntero**.

El compilador solo necesita saber:

- El tamaño de un puntero (p. ej. 8 bytes).
- No necesita saber cómo está construida la clase `Curso`.

---

## ¿Por qué no funciona por valor?

Esto fallaría:

```cpp
Curso curso;   // ❌ error
```

Porque ahora el compilador necesita:

- Saber cuánto mide `Curso`.
- Conocer todos sus atributos.
- Conocer su definición completa.

Y en ese momento todavía no la tiene.

---

## Explicación didáctica para clase

Puedes decirlo así a los estudiantes:

*“La dependencia mutua no es un problema de diseño lógico. Es un problema de orden de compilación. El compilador necesita saber el tamaño real de los objetos antes de usarlos.”*

---

**Referencia (APA):** (Savitch, 2018). Savitch, organización de programas en múltiples archivos; headers y dependencias.
