| <div align="right"><img src="Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Sesión 2 (Estudiantes)

**Duración:** 2 horas  
**Tema:** Downcast y Dependencia mutua

---

## Explicación (resumen)

- **Downcast:** Conversión de base a derivada; no siempre segura. Use `dynamic_cast` y compruebe resultado (por ejemplo `!= nullptr`).
- **Dependencia mutua:** Dos clases que se referencian entre sí. Solución: declaración adelantada (`forward declaration`) y definir métodos en .cpp.

---

## Espacio para tu código

### Ejercicio 1: dynamic_cast

Partiendo de `Vehiculo`/`Automovil`, tome un `Vehiculo*` que apunte a un `Automovil`. Use `dynamic_cast` a `Automovil*` y compruebe si el cast tuvo éxito antes de usar el puntero.

```cpp
// Escriba aquí: main con Vehiculo* apuntando a Automovil y dynamic_cast a Automovil*

```

### Ejercicio 2: Downcast fallido

Pruebe con un `Vehiculo*` que apunte a un objeto que **no** sea `Automovil`. Compruebe que `dynamic_cast<Automovil*>` devuelve `nullptr`.

```cpp
// Escriba aquí el caso donde el downcast falla

```

### Ejercicio 3: Dependencia mutua (Estudiante y Curso)

Dos clases: `Estudiante` (tiene `Curso*`) y `Curso` (tiene `Estudiante*`). Use forward declaration y defina los métodos en el mismo archivo o en .cpp para evitar dependencias circulares.

```cpp
// Forward declaration de Curso
// class Estudiante { ... Curso* curso; ... };
// class Curso { ... Estudiante* estudiante; ... };
// Defina los métodos que usan ambas clases

```

---

## Criterios de validación (para el profesor)

- [ ] Uso de `dynamic_cast` y comprobación de `nullptr`
- [ ] Forward declaration y definiciones que evitan dependencia circular
- [ ] Uso de `using namespace std;`
