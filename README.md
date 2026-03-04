# QA-Manual-Web-Testing
# QA Manual Web Testing & Bug Tracking Portfolio

Este repositorio contiene un proyecto práctico de ejecución de pruebas manuales y Bug Tracking en un entorno E-commerce simulado.

**Entorno de pruebas:** [Sauce Demo (Swag Labs)](https://www.saucedemo.com/)
**Herramientas simuladas:** Jira, Zephyr/Xray.

---

## Bug Reports

Durante la fase de pruebas exploratorias y ejecución de Test Cases con el usuario `problem_user`, se identificaron y categorizaron los siguientes defectos, aplicando criterios de severidad orientados a negocio:

### BUG-001: Bloqueo en la funcionalidad "Add to cart" para productos específicos.
* **Tipo:** Funcional
* **Severidad:** Crítica (Blocker) - Impide la conversión y venta directa.
* **Pasos para reproducir:**
  1. Iniciar sesión con el usuario `problem_user`.
  2. Navegar al catálogo principal (`/inventory.html`).
  3. Hacer clic en el botón "Add to cart" del producto específico *Sauce Labs Bolt T-Shirt* (o *Sauce Labs Fleece Jacket*).
* **Resultado Esperado:** El botón cambia a "Remove", el producto se añade al carrito y el contador superior se actualiza.
* **Resultado Actual:** El botón no responde a la interacción y el producto no se añade al carrito.
* **Notas:** Este error no ocurre con todos los productos (ej. *Sauce Labs Backpack* sí permite ser añadido). 

### BUG-002: Assets visuales incorrectos (imágenes duplicadas) en todo el catálogo.
* **Tipo:** Visual / UI
* **Severidad:** Alta (High) - Fuerte impacto negativo en la imagen de marca y confusión del cliente.
* **Pasos para reproducir:**
  1. Iniciar sesión con el usuario `problem_user`.
  2. Observar la cuadrícula de productos en el inventario.
* **Resultado Esperado:** Cada tarjeta de producto debe mostrar la fotografía correspondiente a su título y descripción.
* **Resultado Actual:** Todas las tarjetas de producto cargan exactamente el mismo asset (la imagen de un perro), sobrescribiendo las imágenes originales del catálogo.

### BUG-003: El filtro de ordenación de productos no aplica ningún criterio.
* **Tipo:** Funcional / Usabilidad.
* **Severidad:** Media/Baja (Minor) - Empeora la experiencia de usuario al buscar productos, pero no bloquea el flujo principal de compra.
* **Pasos para reproducir:**
  1. Iniciar sesión con el usuario `problem_user`.
  2. Navegar al catálogo principal (`/inventory.html`).
  3. Hacer clic en el menú desplegable de ordenación (arriba a la derecha) y seleccionar la opción "Price (low to high)".
* **Resultado Esperado:** La cuadrícula de productos debe actualizarse automáticamente y mostrar los artículos ordenados de menor a mayor precio.
* **Resultado Actual:** El sistema ignora la acción. Los productos mantienen su orden predeterminado alfabético y el filtro visual no se aplica.


# Proyecto 2: Form Validation & Business Logic Testing

Este segundo módulo del portfolio se centra en la validación de formularios complejos, aplicando técnicas formales de diseño de pruebas de software (Caja Negra) para garantizar la integridad de los datos y la robustez del sistema.

**Entorno de pruebas:** [DemoQA Practice Form](https://demoqa.com/automation-practice-form)

## Técnicas de Diseño de Pruebas Aplicadas
Se han ejecutado pruebas exhaustivas utilizando las siguientes metodologías:
1. **Happy Path / Smoke Testing:** Validación del flujo principal de registro.
2. **Boundary Value Analysis (BVA):** Pruebas en los límites exactos de los campos (ej. validación de longitud máxima/mínima en números de teléfono).
3. **Equivalence Partitioning (EP):** Inserción de clases de datos inválidos (letras, caracteres especiales) en campos estrictamente numéricos.
4. **Business Logic Flaw Detection:** Búsqueda de vulnerabilidades en la lógica de negocio y reglas del mundo real.

## Casos de Prueba Destacados (Test Cases)

* **TC-004 [Formulario - Happy Path]:** Registro exitoso con datos válidos en todos los campos obligatorios. (Estado: PASS)
* **TC-005 [Validación - BVA]:** Intento de registro ingresando 9 y 11 dígitos en el campo "Mobile" (límite estricto de 10). El sistema rechaza correctamente el envío. (Estado: PASS)
* **TC-006 [Validación - EP]:** Intento de registro ingresando caracteres alfabéticos (`abcdefghij`) y símbolos (`!@#$%^&*()`) en el campo "Mobile". El sistema bloquea correctamente la entrada de datos no numéricos. (Estado: PASS)

## Bug Report (Defecto Lógico Crítico)

A pesar de que el formulario es técnicamente robusto ante errores de sintaxis, se ha identificado un fallo crítico en la lógica de negocio (*Business Logic Flaw*):

### BUG-004: El campo "Date of Birth" permite registrar usuarios nacidos en el futuro.
* **Tipo:** Lógica de Negocio / Integridad de Datos.
* **Severidad:** Media (Medium) - Corrompe la base de datos con información irreal, afectando a futuras segmentaciones, analíticas o restricciones de edad legal.
* **Pasos para reproducir:**
  1. Navegar al formulario de registro.
  2. Rellenar los campos obligatorios con datos válidos (Nombre, Apellido, Género, Móvil).
  3. Desplegar el calendario en el campo "Date of Birth".
  4. Seleccionar un año en el futuro (ej. Año 2050).
  5. Hacer clic en "Submit".
* **Resultado Esperado:** El sistema debe aplicar una regla de validación de fecha (ej. `max="today"`) y mostrar un mensaje de error indicando que la fecha de nacimiento no puede ser posterior al día actual.
* **Resultado Actual:** El sistema acepta la fecha futura sin restricciones, el registro se completa exitosamente y el modal de confirmación muestra una fecha de nacimiento imposible (ej. 15 Noviembre 2050).
