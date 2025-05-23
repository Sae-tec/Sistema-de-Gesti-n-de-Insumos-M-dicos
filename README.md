# 🏥 Sistema de Entrega de Números de Fila - Clínica

✅ **Descripción General del Sistema**

Este proyecto documenta el modelado completo de un **Sistema de Entrega de Números de Fila**, diseñado para optimizar la atención al paciente en entornos clínicos mediante una gestión ordenada, clara y trazable del flujo de personas. El sistema busca emular los mecanismos de atención por turnos, reduciendo tiempos de espera, evitando aglomeraciones y mejorando la experiencia del usuario.

El modelado abarca los siguientes aspectos críticos:

- Asignación automatizada de números de fila por servicio.
- Llamado de turnos en tiempo real mediante pantallas o interfaces.
- Priorización de turnos especiales (urgencias, adultos mayores, etc.).
- Gestión de tiempos de espera y métricas de atención.
- Acceso por perfiles: pacientes, recepcionistas, supervisores.
- Escalabilidad para múltiples servicios y módulos de atención.

---

🔍 **Objetivos del Modelado**

- Representar el sistema desde una visión funcional hasta el despliegue físico.
- Aplicar patrones de diseño adecuados a los desafíos operativos del sistema.
- Garantizar modularidad, escalabilidad y separación clara de responsabilidades.
- Documentar todos los componentes relevantes sin implementar código.

---

🔹 **1. Diagrama de Casos de Uso UML**

![Image](https://github.com/user-attachments/assets/d46e2189-c127-4d07-ad20-7eef3760e2d8)

### Descripción general

El análisis funcional permitió identificar actores clave y sus respectivas interacciones con el sistema. Se utilizaron relaciones UML (`<<include>>`, `<<extend>>`) para representar flujos obligatorios y opcionales.

**Actores identificados:**

- **Paciente:** Solicita su turno para servicio `<<automatico>>`, consulta posicion en la fila.
- **Recepcionista:** Reasigna turnos, gestion de prioridades especiales.
- **Supervisor:** Generacion de metricas, gestiona modulos y servicios y audita el sistema.

**Casos de uso destacados:**

- Asignacion automatizada por servicio  
  `<<include>>`: Selecciona Servicio   
  `<<include>>`: Generar QR único

- Gestion de Prioridades especiales
  `<<include>>`: Validar criterios de prioridad

- llamado de turnos tiempo real
  `<<extend>>`: Notificar paciente
  `<<extend>>`: Actualizar displays

- Generacion de métricas
  `<<extend>>`: Exportar reportes

- Gestión de módulos y servicios  
  `<<extend>>`: configurar nuevos servicios

**Justificación del modelado:**

Se utilizaron `<<include>>` cuando una acción siempre requiere otra funcionalidad base (ej. Asignacion de servicios que el paciente tiene que seleccionar el servicio obligatorio), y `<<extend>>` cuando la funcionalidad es opcional o condicional (ej. Gestión de módulos y servicios ). Esto permite modelar comportamientos realistas en el sistema de atención por turnos.

---

🔹 **2. Diagrama de Clases UML con Patrones Aplicados**

![Image](https://github.com/user-attachments/assets/2caffe19-b77b-471a-8d32-f0044a8ddd15)

---

🧩 **Justificación Arquitectónica y Patrones Aplicados**

### 1. **Singleton (ConfiguracionTurnos)**
**Justificación:**
Controla parámetros globales del sistema como tipos de servicio, tiempos máximos, prioridad de atención y reglas de turno.

**Objetivo:**
Asegurar una única fuente de verdad para configuraciones compartidas, evitando conflictos o duplicidades.

---

### 2. **Prototype (PlantillaTurno)**
**Justificación:**
Permite generar rápidamente nuevos turnos a partir de plantillas preconfiguradas por tipo de atención (ej. pediatría, urgencia, control).

**Objetivo:**
Agilizar la creación de turnos comunes sin redefinir cada uno desde cero, aumentando la eficiencia operativa.

---

### 3. **Adapter (AdaptadorPantallaExterna)**
**Justificación:**
Integra el sistema con pantallas o quioscos de llamado de turno sin acoplarse directamente a sus APIs o protocolos específicos.

**Objetivo:**
Asegurar la compatibilidad con múltiples dispositivos o software de visualización, manteniendo la independencia del sistema central.

---

### 4. **Bridge (InterfazUsuario + VistaPaciente, VistaRecepcionista)**
**Justificación:**
Separa la lógica del sistema de las interfaces específicas según el tipo de usuario, facilitando adaptaciones a móviles, web o quioscos.

**Objetivo:**
Flexibilizar la interfaz según el contexto de uso, sin duplicar lógica de negocio ni complicar el mantenimiento.

---

🔹 **3. Diagrama de Implementación UML**

![Diagrama de Implementacion](diagramas/Diagrama%20de%20Implementación.png)

### Despliegue Físico y decisiones técnicas:

- Separación en nodos de **interfaz**, **lógica de turnos**, **configuración**, y **visualización externa**.
- Comunicación mediante servicios REST para asegurar escalabilidad y desacoplamiento.
- Módulo de configuración aislado y accesible solo por administradores para evitar modificaciones accidentales.
- Posibilidad de ejecutar instancias paralelas para distintos servicios clínicos o sucursales.

---

🧩 **Reflexiones Finales del Modelado**

Este sistema fue modelado siguiendo criterios profesionales de ingeniería de software, priorizando:

- Coherencia entre los niveles de abstracción: casos de uso ➡ clases ➡ implementación.
- Aplicación de patrones de diseño según la problemática específica, y no como elemento decorativo.
- Modularización clara y capacidad de adaptación futura a nuevos requerimientos (ej. apps móviles, módulos para farmacias).
- Enfoque en la experiencia de usuario tanto para pacientes como operadores.

---
