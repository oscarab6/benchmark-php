# Guía de contribución

Gracias por contribuir al proyecto **benchmark-php**.

Este documento describe cómo preparar el entorno de desarrollo, trabajar con el repositorio, utilizar los hooks, ejecutar las comprobaciones, crear Pull Requests y fusionar cambios en la rama principal.

---
## Índice

- [1. Requisitos previos](#1-requisitos-previos)
- [2. Preparar el entorno de desarrollo](#2-preparar-el-entorno-de-desarrollo)
- [3. Flujo de trabajo con Git](#3-flujo-de-trabajo-con-git)
  - [3.1. Actualizar la rama principal](#31-actualizar-la-rama-principal)
  - [3.2. Crear una rama de trabajo](#32-crear-una-rama-de-trabajo)
  - [3.3. Realizar cambios y commits](#33-realizar-cambios-y-commits)
  - [3.4. Subir los cambios](#34-subir-los-cambios)
  - [3.5. Crear un Pull Request](#35-crear-un-pull-request)
  - [3.6. Contribuciones externas mediante Fork](#36-contribuciones-externas-mediante-fork)
- [4. Convenciones de código](#4-convenciones-de-código)
- [5. Desarrollo de funcionalidades](#5-desarrollo-de-funcionalidades)
- [6. Pruebas y validaciones](#6-pruebas-y-validaciones)
- [7. Revisión de Pull Requests](#7-revisión-de-pull-requests)
- [8. Comunicación y colaboración](#8-comunicación-y-colaboración)
- [9. Agradecimientos](#9-agradecimientos)

---

## 1. Requisitos previos

Antes de comenzar, asegúrate de disponer de las siguientes herramientas:

- Git para el control de versiones.

- PHP 8.3 o superior.

- Extensiones PHP: mbstring, openssl, curl, dom y xml.

- Composer 2 para la gestión de dependencias.

## 2. Preparar el entorno de desarrollo

Clona el repositorio:

```bash
git clone https://github.com/oscarab6/benchmark-php.git
cd benchmark-php
```

Instala las dependencias:
```bash
composer install
```

Activa los hooks de Git configurados en el proyecto:
```bash
git config core.hooksPath .githooks
```

Este último comando debe ejecutarse una sola vez por cada clon del repositorio. El hook de pre-commit ejecutará automáticamente PHP-CS-Fixer para aplicar las correcciones de formato antes de crear un commit.

## 3. Flujo de trabajo con Git

Se utilizará un flujo de trabajo basado en ramas y Pull Requests, **squash and merge**. No se deben realizar cambios directamente sobre la rama main.

### 3.1. Actualizar la rama principal

Antes de comenzar una nueva tarea, actualiza tu repositorio local:
```bash
git switch main
git pull origin main
```

### 3.2. Crear una rama de trabajo

Cada nueva funcionalidad, corrección o modificación debe desarrollarse en una rama independiente.
Se recomienda utilizar los siguientes prefijos:

| Prefijo | Uso |
|---------|-----|
| `feature/` | Nuevas funcionalidades |
| `fix/` | Corrección de errores |
| `docs/` | Cambios en la documentación |
| `test/` | Incorporación o modificación de pruebas. |
| `refactor/` | Mejoras internas del código sin cambiar su comportamiento |

Ejemplos:
```bash
git switch -c feature/mergesort
git switch -c fix/validacion-benchmark
git switch -c docs/actualizacion-readme
```

### 3.3. Realizar cambios y commits

Los commits deben seguir la convención Conventional Commits, utilizando mensajes descriptivos que indiquen claramente el propósito del cambio.

La estructura será:

**tipo(ámbito): descripción breve del cambio**

Los tipos principales que se utilizarán en el proyecto son:
| Tipo | Uso |
|---|---|
| `feat` | Incorporación de nuevas funcionalidades. |
| `fix` | Corrección de errores. |
| `docs` | Cambios en la documentación. |
| `chore` | Tareas de mantenimiento y configuración del proyecto. |
| `test` | Incorporación o modificación de pruebas. |
| `refactor` | Mejoras internas del código sin modificar su comportamiento. |

El ámbito `(scope)` es opcional y permite identificar la parte del proyecto afectada.

**Ejemplos de commits:**
```bash
git commit -m "chore(build): añade PHP-CS-Fixer para formateo automático"
git commit -m "chore(hooks): añade hook de pre-commit con PHP-CS-Fixer"
git commit -m "docs: añade README con instrucciones de uso"
git commit -m "chore: añade plantillas de PR e issues"
git commit -m "chore: añade CODEOWNERS"
git commit -m "docs: añade CONTRIBUTING.md"
```

Se recomienda que los mensajes sean breves, claros y estén redactados en español manera consistente.
Cada commit debe representar un cambio lógico y concreto. Se pueden realizar tantos commits como sean necesarios durante el desarrollo de una tarea.

### 3.4. Subir los cambios

Publica tu rama en GitHub:
```bash
git push -u origin nombre-de-tu-rama
```

### 3.5. Crear un Pull Request

Cuando termines tu trabajo, abre un Pull Request hacia la rama main.
Antes de solicitar la integración, comprueba que:

- Los cambios corresponden al objetivo de la tarea.

- El código cumple las convenciones de estilo.

- No se han introducido archivos innecesarios.

- Se han ejecutado las comprobaciones pertinentes.

- La descripción del Pull Request explica claramente los cambios realizados.

Los Pull Requests deberán superar las comprobaciones automáticas de CI y obtener la revisión y aprobación correspondiente de los propietarios del código.

La integración se realizará mediante Squash and merge, de manera que todos los commits del Pull Request se combinen en un único commit en main.

### 3.6. Contribuciones externas mediante Fork

Los colaboradores externos que no dispongan de permisos de escritura en el repositorio deberán utilizar el flujo de trabajo basado en Forks para proponer cambios.

Este procedimiento permite desarrollar mejoras de forma independiente sin modificar directamente el repositorio original.

#### 3.6.1. Crear un Fork

Accede al repositorio original:

[https://github.com/oscarab6/benchmark-php](https://github.com/oscarab6/benchmark-php)

Pulsa el botón **Fork** de GitHub para crear una copia del repositorio en tu propia cuenta.

#### 2. Clonar el Fork

Clona tu copia personal del repositorio:
```bash
git clone https://github.com/USUARIO/benchmark-php.git
cd benchmark-php
```

Sustituye USUARIO por tu nombre de usuario de GitHub.

#### 3. Configurar el repositorio original como upstream

Añade el repositorio original como remoto para poder sincronizar los cambios:
```bash
git remote add upstream https://github.com/oscarab6/benchmark-php.git
```

Puedes comprobar los remotos configurados mediante:
```bash
git remote -v
```

#### 4. Actualizar la rama principal y crear una rama de trabajo

Sincroniza tu rama principal con los últimos cambios del repositorio original:
```bash
git fetch upstream
git switch main
git merge upstream/main
```

Crea una rama independiente para tu contribución:
```bash
git switch -c feature/nueva-funcionalidad
```

#### 5. Realizar los cambios

Implementa la funcionalidad, corrección o mejora siguiendo las convenciones de código y commits establecidas en este documento.

Comprueba que los cambios funcionan correctamente antes de enviarlos.

#### 6. Subir los cambios a tu Fork

Publica tu rama en tu repositorio personal:
```bash
git push -u origin feature/nueva-funcionalidad
```

#### 7. Crear un Pull Request

Accede a GitHub y crea un Pull Request desde tu rama del Fork hacia el repositorio original.

Comprueba que la configuración sea:

- Base repository: oscarab6/benchmark-php.

- Base branch: main.

- Head repository: tu Fork personal.

- Compare branch: feature/nueva-funcionalidad.

Describe los cambios realizados y explica por qué consideras que deberían incorporarse al proyecto.

#### 8. Revisión e integración

El equipo mantenedor revisará la propuesta, podrá solicitar modificaciones y comprobará que se cumplen los requisitos del proyecto.

Si el Pull Request es aprobado y supera las comprobaciones correspondientes, se integrará en main mediante **Squash and merge**.

No es necesario disponer de permisos de escritura en el repositorio original para realizar este procedimiento.

## 4. Convenciones de código

El proyecto sigue las convenciones de estilo PSR-12 de PHP. Para mantener la uniformidad del código se utiliza PHP-CS-Fixer. Antes de enviar los cambios, puedes comprobar el formato mediante:
```bash
composer cs:check
```

Si necesitas corregir automáticamente el formato:
```bash
composer cs:fix
```

Ten en cuenta que el hook de pre-commit también ejecuta las correcciones de formato automáticamente.

## 5. Desarrollo de funcionalidades

Al implementar nuevas funcionalidades:

- Mantén una estructura de código clara y organizada.

- Utiliza nombres descriptivos para clases, métodos y variables.

- Evita duplicar código cuando pueda reutilizarse una implementación existente.

- Gestiona adecuadamente los errores y las entradas no válidas.

- Mantén la compatibilidad con PHP 8.3 o superior.

- Respeta el contrato de la API acordado con el resto de los grupos del proyecto.

Las nuevas implementaciones de algoritmos deben mantener un comportamiento correcto y permitir evaluar su rendimiento de forma consistente.

## 6. Pruebas y validaciones

Los cambios deben comprobarse antes de solicitar su integración.

Como mínimo, ejecuta las comprobaciones de formato:
```bash
composer cs:check
```

Cuando se incorporen pruebas automatizadas al proyecto, deberán ejecutarse también antes de abrir el Pull Request.
Las nuevas funcionalidades deben incluir pruebas que permitan verificar su comportamiento y detectar posibles regresiones.

## 7. Revisión de Pull Requests

Todos los cambios deben integrarse mediante Pull Requests.

Durante la revisión:

- Los colaboradores pueden comentar y proponer mejoras.

- El autor debe atender las observaciones recibidas.

- Los propietarios del código revisarán los cambios correspondientes.

- No se debe integrar un Pull Request que tenga comprobaciones obligatorias fallidas o revisiones pendientes.

Una vez aprobado y validado, se utilizará **Squash and merge** para integrarlo en main.

## 8. Comunicación y colaboración

Si tienes dudas sobre una implementación, encuentras un error o quieres proponer una mejora:

- Consulta primero los Issues existentes.

- Si no existe uno relacionado, abre un nuevo Issue describiendo el problema o la propuesta.

- Evita duplicar tareas o implementar cambios que puedan entrar en conflicto con el trabajo de otros colaboradores.

- Coordina con el equipo cualquier modificación que afecte al contrato de la API compartida.

## 9. Agradecimientos

Gracias a todos los colaboradores que participan en el desarrollo de Benchmark PHP.
La colaboración, la revisión del código y el cumplimiento de estas pautas ayudan a mantener un proyecto organizado, mantenible y de calidad.