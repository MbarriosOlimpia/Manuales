# 🗂️ Api Servicio Histórico de Clases

**Documentación Técnica — Versión 1.0.0**

---

## 📋 Contenido

1. [Control de Cambios](#1-control-de-cambios)
2. [Introducción](#2-introducción)
3. [Objetivo](#3-objetivo)
4. [Alcance](#4-alcance)
5. [Cargo Responsable](#5-cargo-responsable-del-procedimiento)
6. [Roles Involucrados](#6-roles-involucrados-en-el-procedimiento)
7. [Listado Histórico de Clases Teóricas y Prácticas](#7-listado-histórico-de-clases-teóricas-y-prácticas)
8. [Observaciones](#8-observaciones)
9. [Propiedad de Olimpia](#9-propiedad-de-olimpia)

---

## 1. 📝 Control de Cambios

| Versión | Fecha      | Descripción                                                                                             |
| ------- | ---------- | ------------------------------------------------------------------------------------------------------- |
| 1.0     | 2026-03-31 | Creación del documento.                                                                                 |
| 1.0     | 2026-03-31 | Se agrega información del método para: Listar histórico de clases teóricas y prácticas de un aspirante. |

---

## 2. 📖 Introducción

Este documento técnico ha sido diseñado como una guía para la integración y el consumo del servicio de Histórico de Clases. En él se detallan los lineamientos necesarios para consultar la información referente a las sesiones teóricas y prácticas que un aspirante ha completado.

El documento actúa como la fuente oficial de verdad para asegurar que la comunicación entre el backend y la interfaz de usuario sea fluida, permitiendo una representación fiel del progreso académico del usuario en la plataforma.

---

## 3. 🎯 Objetivo

Proporcionar a los equipos de desarrollo y aseguramiento de calidad (QA) todos los insumos técnicos, definiciones de parámetros y reglas de negocio necesarios para:

- Implementar el consumo del servicio de forma eficiente en el producto **Mi Licencia**.
- Visualizar correctamente el listado de clases finalizadas, garantizando la integridad de los datos mostrados al aspirante.
- Validar mediante pruebas de QA que el servicio responde a los criterios de aceptación y flujos de error previstos.

---

## 4. 🔍 Alcance

El presente documento abarca los siguientes puntos:

- **Definición del Servicio:** Descripción de los endpoints y métodos de consulta para el histórico de clases teóricas y prácticas.
- **Interacción de Datos:** Especificación de los modelos de entrada (request) y salida (response).
- **Contexto de Aplicación:** El uso exclusivo dentro del ecosistema del producto Mi Licencia.
- **Criterios de Validación:** Guía básica para que el equipo de QA pueda verificar la correcta recepción y renderizado de las clases finalizadas.

> **Nota:** Este documento no cubre la lógica de agendamiento de clases ni la gestión de pagos, enfocándose exclusivamente en la consulta de clases ya concluidas.

---

## 5. 👤 Cargo Responsable del Procedimiento

Ingeniero desarrollo CEA

---

## 6. 👥 Roles Involucrados en el Procedimiento

| Rol           | Cargo                   |
| ------------- | ----------------------- |
| Desarrollador | Ingeniero de desarrollo |

---

## 7. 📊 Listado Histórico de Clases Teóricas y Prácticas

### 7.1. ℹ️ Información General del Servicio

**URL del servidor** (según ambiente):

| Ambiente       | Dirección                     |
| -------------- | ----------------------------- |
| Dev            | `http://olsrvdesapceia1:6270` |
| Pruebas        | `http://olsrvpruapceia1:6270` |
| Pre-producción | `http://olnlbpreapceia1:9120` |
| Producción     | `http://olnlbproapceia1:9120` |

**🔗 URL del servicio:**

```
/json/aspirante/tipoIdentificacion/{tipoDocumento}/numero/{numeroDocumento}/categoria/{categoria}/historialclases
```

**📌 Ejemplos:**

```
http://localhost:63347/MiLicencia/ServicioTransaccional.svc/JSON/aspirante/tipoIdentificacion/CO/numero/33104191/categoria/A2/historialclases
http://localhost:63347/MiLicencia/ServicioTransaccional.svc/JSON/aspirante/tipoIdentificacion/10/numero/33104191/categoria/2/historialclases
```

---

### 7.2. 🔒 Autenticación

El servicio **no requiere autenticación**.

---

### 7.3. 🔗 Endpoints

#### 7.3.1. 📋 Listado Histórico de Clases

Método para listar clases teóricas y prácticas en estado **finalizado** de un aspirante.

- **Método:** `GET`
- **Endpoint:**

```
/aspirante/tipoIdentificacion/{tipoDocumento}/numero/{numeroDocumento}/categoria/{categoria}/historialclases
```

- **Ejemplo:**

```
/aspirante/tipoIdentificacion/10/numero/33104191/categoria/2/historialclases
```

---

#### 7.3.1.1. ⚠️ Parámetros Obligatorios

Todos los parámetros incluidos en la URL.

---

#### 7.3.1.2. 🔘 Parámetros Opcionales

N/A

---

#### 7.3.1.3. 📢 Mensajes en Caso de Error

| Casuística              | Código HTTP | Texto                                                                                                                                                           |
| ----------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tipo documento inválido | 200         | `"El tipo de documento 'CeO' no es válido. Los tipos de documento permitidos son: CC, CE, TI, N, PP, CO, CA, TR, Y."`                                           |
| Tipo documento inválido | 200         | `"El IdTipoIdentificacion '34' no es válido. Los IdTipoIdentificacion permitidos son: 1, 2, 3, 4, 5, 8, 10, 11, 12, 13."`                                       |
| Categoría inválida      | 200         | `"La categoría 'A2w' no es válida. Las categorías permitidas son: A1, A2, B1, C1, B2, C2, B3, C3, Curso, Todos, RC1, IA1, IA2, IB1, IC1, IB2, IC2, IB3, IC3."` |
| Categoría inválida      | 200         | `"El IdCategoria '34' no es válido. Los IdCategoria permitidos son: 1, 2, 3, 4, 5, 6, 7, 9, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27."`                      |

---

#### 7.3.1.4. ✍️ Request

| Nombre          | Tipo de dato | Observación                                                                                                                                  |
| --------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| tipoDocumento   | string       | El dato debe poder convertirse a entero; en caso contrario, el texto debe estar dentro de los códigos de los tipos de documento permitidos.  |
| categoria       | string       | El dato debe poder convertirse a entero; en caso contrario, el texto debe estar dentro de los códigos de las categorías permitidas.          |
| numeroDocumento | string       | Identificador del estudiante.                                                                                                                |

---

#### 7.3.1.5. 📤 Response

La solicitud responde un JSON con el siguiente formato:

- **Data:** Contiene el objeto respuesta de la petición.
  - **ClasesPracticas:** Listado de objetos con información de la clase práctica finalizada.
  - **ClasesTeoricas:** Listado de objetos con información de la clase teórica finalizada.
- **Message:** Retorna el mensaje en caso de ocurrir alguna excepción.
- **TotalItems:** Número total de registros devueltos.

| Nombre               | Tipo de dato | Observación                                       |
| -------------------- | ------------ | ------------------------------------------------- |
| Data                 | object       | Objeto de respuesta.                              |
| Data:ClasesPracticas | List         | Listado de clases prácticas finalizadas.          |
| Data:ClasesTeoricas  | List         | Listado de clases teóricas finalizadas.           |
| message              | String       | Mensaje de respuesta en caso de existir un error. |
| TotalItems           | Int          | Cantidad total de registros devueltos.            |

---

### 📄 JSON de Apoyo: ✅ Response OK

```json
{
    "Data": {
        "ClasesPracticas": [
            {
                "FechaClase": "Martes 16 de diciembre de 2025",
                "NombreProfesor": "MAYRA  BARRIOS",
                "PlacaVehiculo": "YHK77F"
            },
            {
                "FechaClase": "Jueves 26 de junio de 2025",
                "NombreProfesor": "MAYRA  BARRIOS",
                "PlacaVehiculo": "YHK77F"
            }
        ],
        "ClasesTeoricas": [
            {
                "FechaClase": "Viernes 6 de diciembre de 2024",
                "NombreAula": "Aula Teórica",
                "NombreClase": "Adaptación al Medio 2 Todas categorías",
                "NombreProfesor": "MAYRA  BARRIOS"
            },
            {
                "FechaClase": "Miércoles 20 de marzo de 2024",
                "NombreAula": "Aula Teórica",
                "NombreClase": "Adaptación al Medio 2 Todas categorías",
                "NombreProfesor": "MAYRA  BARRIOS"
            }
        ]
    },
    "Message": "",
    "TotalItems": 4
}
```

---

### 📄 JSON de Apoyo: ✅ Response con un Solo Listado

```json
{
    "Data": {
        "ClasesPracticas": [],
        "ClasesTeoricas": [
            {
                "FechaClase": "Viernes 6 de diciembre de 2024",
                "NombreAula": "Aula Teórica",
                "NombreClase": "Adaptación al Medio 2 Todas categorías",
                "NombreProfesor": "MAYRA  BARRIOS"
            },
            {
                "FechaClase": "Miércoles 20 de marzo de 2024",
                "NombreAula": "Aula Teórica",
                "NombreClase": "Adaptación al Medio 2 Todas categorías",
                "NombreProfesor": "MAYRA  BARRIOS"
            }
        ]
    },
    "Message": "",
    "TotalItems": 2
}
```

---

### 📄 JSON de Apoyo: 🚩 Response con Error

```json
{
    "Data": {
        "ClasesPracticas": [],
        "ClasesTeoricas": []
    },
    "Message": "La categoría 'Bg1' no es válida. Las categorías permitidas son: A1, A2, B1, C1, B2, C2, B3, C3, Curso, Todos, RC1, IA1, IA2, IB1, IC1, IB2, IC2, IB3, IC3.\r\nNombre del parámetro: cat",
    "TotalItems": 0
}
```

---

## 8. 💡 Observaciones

- Los datos suministrados del aspirante en los ejemplos son de ambientes de desarrollo. Se recomienda usar información de acuerdo con el ambiente donde se esté ejecutando el servicio.

---

## 9. ©️ Propiedad de Olimpia

El presente documento es de carácter confidencial y está protegido por las normas de derechos de autor. Cualquier reproducción, distribución o modificación total o parcial a usuarios no autorizados, o cualquier uso indebido de la información confidencial, será considerado un delito conforme a lo establecido por el Código Penal y Leyes vigentes del estado Colombiano.

---

*OlimpIA · Documentación Técnica · 2026 — Documento de uso interno. © Todos los derechos reservados.*