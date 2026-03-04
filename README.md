# QA-Manual-Web-Testing
# 🛒 QA Manual Web Testing & Bug Tracking Portfolio

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
