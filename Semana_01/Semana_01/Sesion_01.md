| <div align="right"><img src="Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Sesión 1 (Sesión 1)

**Duración:** 2 horas  
**Tema:** Relaciones – repaso y Upcast

---

## Explicación

- **Relaciones entre clases (repaso):** Se repasan los tipos de relación en POO: generalización (herencia), dependencia (uso temporal) y asociación (agregación y composición). Es fundamental distinguir "es-un" (herencia) de "tiene-un" (composición/agregación).
- **Upcast (conversión ascendente):** Es la conversión de una referencia o puntero de una clase derivada a su clase base. Es segura y puede ser implícita: un objeto de la clase derivada *es* también un objeto de la clase base. Se usa para tratar distintos tipos derivados de forma uniforme mediante la interfaz de la base (polimorfismo).

**Referencia (APA):** (Savitch, 2018). Savitch, capítulos sobre herencia y clases base/derivadas; uso de punteros/referencias a clase base.

**Sección general:** Ver material de apoyo ampliado en [Sección general – Relaciones entre clases y Upcast](Generales/Seccion_General_Relaciones_Upcast.md) (repaso es-un / tiene-un / usa-a, upcast, polimorfismo y pregunta para evaluar en clase).

---

## Ejemplos de código C++ para la clase

Todos los ejemplos usan `using namespace std;` para simplificar la exposición.

### Ejemplo 1: Relación "es-un" y upcast implícito

```cpp
#include <iostream>
using namespace std;

class Vehiculo {
public:
    void arrancar() { cout << "Vehiculo arrancado.\n"; }
    virtual void describir() { cout << "Soy un vehiculo.\n"; }
};

class Automovil : public Vehiculo {
public:
    void describir() override { cout << "Soy un automovil.\n"; }
};

int main() {
    Automovil a;
    a.arrancar();  // heredado

    // Upcast: puntero derivado -> base (implícito y seguro)
    Vehiculo* pV = &a;
    pV->arrancar();
    pV->describir();  // polimorfismo: "Soy un automovil"

    // Upcast: referencia
    Vehiculo& rV = a;
    rV.describir();
    return 0;
}
```

### Ejemplo 2: Jerarquía de 3 niveles y upcast en cada nivel

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void hablar() { cout << "Sonido generico.\n"; }
};

class Mamifero : public Animal {
public:
    void hablar() override { cout << "Mamifero.\n"; }
};

class Perro : public Mamifero {
public:
    void hablar() override { cout << "Guau!\n"; }
};

int main() {
    Perro p;
    Animal* a = &p;      // upcast nivel 2
    Mamifero* m = &p;    // upcast nivel 1
    a->hablar();         // "Guau!" (polimorfismo)
    m->hablar();         // "Guau!"
    return 0;
}
```

### Ejemplo 3: Array de punteros a base (tratar derivados de forma uniforme)

```cpp
#include <iostream>
using namespace std;

const int MAX_FIGURAS = 10;

class Figura {
public:
    virtual double area() const = 0;
    virtual ~Figura() = default;
};

class Circulo : public Figura {
    double r;
public:
    Circulo(double radio) { r = radio; }
    double area() const override { return 3.14159 * r * r; }
};

class Rectangulo : public Figura {
    double b, h;
public:
    Rectangulo(double base, double alt) {
        b = base;
        h = alt;
    }
    double area() const override { return b * h; }
};

int main() {
    Figura* figuras[MAX_FIGURAS];
    int numFiguras = 0;
    figuras[numFiguras++] = new Circulo(1.0);
    figuras[numFiguras++] = new Rectangulo(2.0, 3.0);

    for (int i = 0; i < numFiguras; i++)
        cout << "Area: " << figuras[i]->area() << endl;

    for (int i = 0; i < numFiguras; i++)
        delete figuras[i];
    return 0;
}
```

---

## Ejercicios de tarea

1. Defina dos clases: `Vehiculo` (base) y `Automovil` (derivada). En `main`, cree un `Automovil` y asígnelo a un puntero o referencia a `Vehiculo`. Justifique por qué esto es upcast y es seguro.
2. Escriba un pequeño programa con una jerarquía de 3 niveles (base → derivada1 → derivada2). Realice upcast en cada nivel a la clase base y muestre que se puede llamar un método definido en la base.
3. Explique en 3–5 líneas por qué el upcast es la base del polimorfismo cuando se usan referencias o punteros a la clase base.
