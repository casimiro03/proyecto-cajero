# proyecto-cajero

deje la carrera para ser autodidacta 0_0, pero aca estoy subiendo esto para que mis amigos tengan una fuente de verdad para que no esteen tan perdidos respecto a lo que se debe hacer

---
![Architecture Diagram](<img width="585" height="615" alt="Pipeline 2026-06-23 17 13 55 excalidraw" src="https://github.com/user-attachments/assets/0f50736c-124e-4d2e-901a-bad16b3607e7" />
)

---
## Descripción general

El sistema emula las operaciones básicas de un cajero automático bancario. El usuario inicia sesión con su DNI y PIN, y accede a un menú interactivo desde donde puede consultar su saldo, extraer efectivo, depositar dinero, transferir fondos a otras cuentas del banco, visualizar el historial de operaciones realizadas y cambiar su PIN.

La sesión cuenta con un límite de 3 intentos fallidos de ingreso, tras los cuales la tarjeta se bloquea temporalmente. Todas las operaciones están validadas: control de saldo insuficiente, límites de extracción y transferencia, formato de montos (incluyendo separador argentino con coma decimal), confirmación previa a cada operación, y registro timestampado de cada transacción en el historial del usuario.

---

## Funcionalidades

| # | Operación | Descripción |
|---|-----------|-------------|
| 1 | Inicio de sesión | Validación de DNI (7-8 dígitos) y PIN (4 dígitos). Máximo 3 intentos. |
| 2 | Consultar saldo | Muestra el titular y el saldo disponible. |
| 3 | Extraer dinero | Controla límite diario ($50.000), saldo suficiente y confirma antes de dispensar. |
| 4 | Depositar dinero | Acredita el monto ingresado al saldo de la cuenta. |
| 5 | Transferir | Valida DNI destino (existente, distinto al origen), límite ($100.000) y saldo. |
| 6 | Ver últimas operaciones | Muestra hasta 10 operaciones recientes con fecha, tipo, monto y saldo posterior. |
| 7 | Cambiar PIN | Requiere PIN actual, permite ingreso del nuevo con confirmación. |
| 8 | Salir | Finaliza la sesión y pregunta si se desea realizar otra operación con otra tarjeta. |

---

## Diagrama de arquitectura

![Pipeline](Pipeline%202026-06-23%2017.13.55.excalidraw.png)

---

## Estructura del proyecto

```
project/
├── cajero.py        # Punto de entrada. Menú principal y ciclo de sesión.
├── datos.py         # Capa de datos. Usuarios en memoria, límites, historial.
├── operaciones.py   # Lógica de cada operación bancaria.
└── utilidades.py    # Validaciones, formato de moneda, entrada de datos.
```

### Módulos

**`cajero.py`** — Contiene la función `main()`, el ciclo de inicio de sesión (`iniciar_sesion`), el menú principal y el bucle de ejecución de la sesión (`ejecutar_sesion`). Orquesta los otros módulos.

**`datos.py`** — Base de datos simulada en memoria. Almacena usuarios con nombre, PIN, saldo e historial de operaciones. Expone funciones para verificar existencia, validar PIN, obtener/actualizar saldo y PIN, y registrar operaciones con fecha y hora.

**`operaciones.py`** — Implementa las 7 operaciones del cajero: consultar saldo, extraer dinero, depositar, transferir, ver historial y cambiar PIN. Cada función maneja su propia validación, confirmación y registro en el historial.

**`utilidades.py`** — Funciones transversales: validación de DNI, validación de PIN, validación y conversión de montos (con soporte para coma decimal), formateo de montos al estándar argentino ($ X.XXX,XX), entrada segura de montos con opción de cancelación, y confirmación de operaciones.

---

## Usuarios de prueba

El sistema incluye 3 cuentas precargadas para pruebas:

| DNI | Nombre | PIN | Saldo inicial |
|-----|--------|-----|---------------|
| 12345678 | Ana García | 1234 | $ 150.000,00 |
| 87654321 | Carlos López | 5678 | $ 32.500,50 |
| 11223344 | María Rodríguez | 9999 | $ 5.000,00 |

---

## Instrucciones de ejecución

### Requisitos

- Python 3.6 o superior.
- No requiere dependencias externas. Solo la biblioteca estándar.

### Pasos

```bash
git clone <url-del-repositorio>
cd pyproject-utn/project
python cajero.py
```

### Flujo de uso

1. Ejecutar `python cajero.py`.
2. Ingresar un DNI válido (ej: `12345678`).
3. Ingresar el PIN correspondiente (ej: `1234`).
4. Seleccionar la operación deseada del menú principal.
5. Seguir las instrucciones en pantalla.
6. Para salir, seleccionar `0` en el menú.
7. El sistema preguntará si desea realizar otra operación con una tarjeta diferente.

---

## Uso de Inteligencia Artificial

*[Completar con las herramientas de IA utilizadas, para qué se usaron y cómo se integraron al desarrollo.]*

Ejemplo: GitHub Copilot, ChatGPT, Claude, agentes multi-sistema para generación de código y pruebas (pytest), etc.

---

## Integrantes

| Nombre | Rol |
|--------|-----|
| *[Nombre]* | *[Rol]* |
| *[Nombre]* | *[Rol]* |
| *[Nombre]* | *[Rol]* |
| *[Nombre]* | *[Rol]* |

**Comisión:** *[Comisión]*
