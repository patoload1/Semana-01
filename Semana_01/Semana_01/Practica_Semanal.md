| <div align="right"><img src="Logo-UNA-Rojo_FondoTransparente%20(2).png" width="120" alt="Logo UNA" /></div> | | <p align="right"><img src="images.jpeg" width="120" alt="Logo EscINF" /></p> |
|:----------------------------------------------------|:-------------------------------------------------------------:|------------------------------------------------------------:|

**Programa de curso** · **Programación II**  
**Carrera:** Ingeniería de Sistemas de Información con grado en Bachillerato y salida lateral de Diplomado en Programación de Aplicaciones Informáticas.

---

# Semana 1 – Práctica semanal

**Contenidos:** Relaciones (repaso), Upcast, Downcast, Dependencia mutua.

---

## Actividad 1 (relaciones y upcast)

- Defina una jerarquía: `Animal` (base) → `Mamifero` → `Perro`.
- En `main`, cree un `Perro` y asígnelo a `Animal*` y a `Mamifero*`. Llame un método definido en `Animal` desde cada puntero.
- Justifique en el archivo MD qué tipo de relación existe entre las clases y por qué el upcast es seguro.

---

## Actividad 2 (downcast)

- Con la jerarquía anterior, tenga un `Animal*` que en tiempo de ejecución apunte a un `Perro`.
- Use `dynamic_cast` a `Perro*` y, si el cast tiene éxito, llame un método específico de `Perro`. Si falla, imprima un mensaje.
- Pruebe también con un `Animal*` que apunte a un `Mamifero` (no a `Perro`) y compruebe que el downcast a `Perro*` falla.

---

## Actividad 3 (dependencia mutua)

- Modele `Autor` (tiene nombre y lista de `Libro*`) y `Libro` (tiene título y `Autor*`).
- Use forward declarations en los headers y defina los métodos en .cpp para evitar dependencias circulares.
- Entregue los archivos .h, .cpp y un breve párrafo en MD explicando la solución.

---

**Formato de entrega:** Código en los archivos correspondientes y respuestas/explicaciones en **archivo(s) MD (Markdown)**.
