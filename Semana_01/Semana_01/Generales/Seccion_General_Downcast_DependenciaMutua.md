| <div align="right"><img src="../Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="../images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Sección general: Downcast y Dependencia mutua

Material de apoyo para la Sesión 2.

---

## 1. ¿Qué es Downcast?

El **downcast** (conversión descendente) ocurre cuando tomamos un puntero o referencia de la clase base y lo convertimos en un puntero o referencia de una clase derivada.

Es lo contrario del upcast.

**Recordatorio:**

- **Upcast:** Derivada → Base (seguro, implícito)
- **Downcast:** Base → Derivada (no siempre seguro)

### ¿Por qué no siempre es seguro?

Porque un puntero a la clase base no garantiza que el objeto real sea de la clase derivada.

**Ejemplo conceptual:**

```cpp
Vehiculo* p = new Vehiculo();
```

Aquí `p` apunta a un objeto `Vehiculo` puro.

Si intentamos:

```cpp
Automovil* a = (Automovil*) p;   // ❌ peligroso
```

Estamos diciendo: *“Confío en que este Vehiculo realmente es un Automovil”*. Pero no lo es. Eso genera **comportamiento indefinido**.

### ¿Cómo se hace seguro el downcast?

En C++ usamos **`dynamic_cast`**.

**Requisitos:**

- La clase base debe tener al menos un método virtual.
- RTTI (Run Time Type Information) debe estar activo.

### Ejemplo explicado paso a paso

```cpp
Vehiculo* p = new Automovil();
```

- Aunque el tipo del puntero es `Vehiculo*`, el objeto real en memoria es `Automovil`.

Ahora hacemos:

```cpp
Automovil* a = dynamic_cast<Automovil*>(p);
```

**¿Qué hace `dynamic_cast`?**

- ✔ Verifica en tiempo de ejecución
- ✔ Pregunta: “¿El objeto real es Automovil?”
- ✔ Si sí → devuelve el puntero convertido
- ✔ Si no → devuelve `nullptr`

**Caso exitoso:**

```cpp
if (a != nullptr) {
    a->soloAutomovil();
}
```

Aquí el cast funciona porque el objeto real era `Automovil`.

**Caso fallido:**

```cpp
Vehiculo* p2 = new Vehiculo();
Automovil* a2 = dynamic_cast<Automovil*>(p2);
```

- El objeto real es `Vehiculo`, no es `Automovil`.
- `dynamic_cast` devuelve `nullptr`.
- Eso evita errores graves.

**Idea clave para clase:**  
*“El upcast es seguro porque todo Automóvil es un Vehículo. El downcast no es seguro porque no todo Vehículo es un Automóvil.”*

---

## 2. Dependencia mutua (referencias circulares)

Ocurre cuando:

- Clase A usa Clase B
- Clase B usa Clase A

**Ejemplo típico:**

- Estudiante → Curso  
- Curso → Estudiante  

Si ponemos en un archivo `#include "Curso.h"` y dentro de `Curso` tenemos `#include "Estudiante.h"`, se produce **dependencia circular**.

### ¿Cómo se resuelve?

Con **forward declaration** (declaración adelantada):

```cpp
class Curso;   // declaración adelantada
```

Esto le dice al compilador: *“Existe una clase llamada Curso, no necesito saber aún cómo es.”*

Luego se usa puntero:

```cpp
Curso* curso;
```

Esto funciona porque el compilador solo necesita saber el tamaño del puntero, no el contenido completo de la clase.

**¿Por qué no funciona con objetos por valor?**

```cpp
Curso curso;  // ❌ error
```

Porque el compilador necesita conocer el tamaño completo del objeto.

**Explicación didáctica:**  
*“La dependencia mutua no es un problema de lógica, es un problema de compilación. El compilador necesita orden.”*

---

## Comparación rápida

| Concepto | ¿Seguro? | ¿Cuándo usarlo? |
|----------|-----------|-----------------|
| Upcast | Sí | Polimorfismo |
| Downcast con `dynamic_cast` | Sí (si se verifica) | Acceder a comportamiento específico |
| Downcast estilo C | No | Nunca recomendado |
| Forward declaration | Sí | Evitar dependencia circular |

---

## Pregunta para evaluación

¿Por qué `dynamic_cast` devuelve `nullptr` y no genera error de compilación cuando el objeto no es del tipo esperado?

---

**Referencia (APA):** (Savitch, 2018). Savitch, herencia y casting; organización de programas en múltiples archivos.
