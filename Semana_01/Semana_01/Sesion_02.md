| <div align="right"><img src="Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Sesión 2 (Sesión 2)

**Duración:** 2 horas  
**Tema:** Downcast y Dependencia mutua

---

## Explicación

- **Downcast (conversión descendente):** Es la conversión de una referencia o puntero de clase base a clase derivada. No siempre es segura: solo tiene sentido cuando el objeto referenciado es realmente de esa clase derivada. En C++ se usa `dynamic_cast` cuando hay funciones virtuales (RTTI) para hacer un downcast seguro; si falla, devuelve `nullptr`.
- **Dependencia mutua (referencias circulares):** Ocurre cuando la clase A usa a B y B usa a A (incluyendo headers). Se resuelve con declaraciones adelantadas (`forward declaration`) y separando declaración de definición; a veces conviene extraer una interfaz o reordenar dependencias.

**Referencia (APA):** (Savitch, 2018). Savitch, herencia y casting; organización de programas en múltiples archivos.

**Sección general:** Ver material de apoyo ampliado en [Sección general – Downcast y Dependencia mutua](Generales/Seccion_General_Downcast_DependenciaMutua.md) (resumen didáctico, comparación upcast/downcast y pregunta de evaluación) y en [Sección general – Dependencia mutua (referencias circulares)](Generales/Seccion_General_DependenciaMutua.md) (ejemplo Estudiante/Curso, forward declaration en .h/.cpp, por qué punteros sí y valor no).

---

## Ejemplos de código C++ para la clase

Todos usan `using namespace std;`.

### Ejemplo 1: dynamic_cast para downcast seguro

```cpp
#include <iostream>
using namespace std;

class Vehiculo {
public:
    virtual ~Vehiculo() = default;
    virtual void tipo() { cout << "Vehiculo\n"; }
};

class Automovil : public Vehiculo {
public:
    void tipo() override { cout << "Automovil\n"; }
    void soloAutomovil() { cout << "Solo los automoviles tienen esto.\n"; }
};

int main() {
    Vehiculo* p = new Automovil();
    p->tipo();

    // Downcast seguro con dynamic_cast
    Automovil* a = dynamic_cast<Automovil*>(p);
    if (a != nullptr) {
        a->soloAutomovil();
    }

    Vehiculo* p2 = new Vehiculo();
    Automovil* a2 = dynamic_cast<Automovil*>(p2);
    if (a2 == nullptr)
        cout << "Downcast fallo: no es Automovil.\n";

    delete p;
    delete p2;
    return 0;
}
```

### Ejemplo 2: Downcast fallido (nullptr)

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual ~Base() = default;
};

class Derivada : public Base {};

int main() {
    Base b;
    Derivada* d = dynamic_cast<Derivada*>(&b);
    if (d == nullptr)
        cout << "Correcto: &b no es un Derivada, cast devuelve nullptr.\n";
    return 0;
}
```

### Ejemplo 3: Dependencia mutua con forward declaration (un solo archivo)

```cpp
#include <iostream>
#include <string>
using namespace std;

class Curso;  // forward declaration

class Estudiante {
    string nombre;
    Curso* curso;
public:
    Estudiante(const string& n) : nombre(n), curso(nullptr) {}
    void inscribir(Curso* c);
    void mostrarCurso() const;
};

class Curso {
    string titulo;
    Estudiante* estudiante;
public:
    Curso(const string& t) : titulo(t), estudiante(nullptr) {}
    void asignarEstudiante(Estudiante* e) { estudiante = e; }
    string getTitulo() const { return titulo; }
};

void Estudiante::inscribir(Curso* c) {
    curso = c;
    c->asignarEstudiante(this);
}
void Estudiante::mostrarCurso() const {
    if (curso)
        cout << nombre << " cursa: " << curso->getTitulo() << endl;
}

int main() {
    Estudiante e("Ana");
    Curso c("Programacion 2");
    e.inscribir(&c);
    e.mostrarCurso();
    return 0;
}
```

---

## Ejercicios de tarea

1. Partiendo de su jerarquía `Vehiculo`/`Automovil`, tome un puntero a `Vehiculo` que en tiempo de ejecución apunte a un `Automovil`. Use `dynamic_cast` a `Automovil*` y compruebe si el cast tuvo éxito antes de usar el puntero.
2. Escriba dos clases que se referencien mutuamente (por ejemplo, `Estudiante` que tiene `Curso*` y `Curso` que tiene `Estudiante*`). Use declaraciones adelantadas y defina los métodos en archivos .cpp para evitar dependencias circulares en los headers.
3. Investigue y redacte un párrafo corto: ¿en qué situaciones es necesario el downcast y por qué debe preferirse `dynamic_cast` frente a un cast estilo C en jerarquías polimórficas?
