Set-Content -Path "c:\Users\juanj\Downloads\asistente.chat\README.md" -Value @'
# 🗂️ Asistente de Tareas SENA

> Aplicativo web desarrollado en Angular para la gestión de tareas con autenticación, persistencia de datos e integración de inteligencia artificial. Proyecto formativo del Programa Tecnólogo en Análisis y Desarrollo de Software - Ficha 3203082.

---

## 📑 Información del Proyecto

**Centro de Formación:** Centro de Biotecnología Agropecuario  
**Programa:** Tecnólogo en Análisis y Desarrollo de Software  
**Ficha:** 3203082  
**Fase del Proyecto:** Ejecución  
**Instructor(a):** Yennifer Steffi Velandia Soto  
**Aprendiz:** Juan Jose Bocanegra  
**Documento de Identidad:** 1141118966 T.I.  
**Fecha de Elaboración:** 23/04/2026  
**Fecha de Inicio:** 23/04/2026  
**Fecha Límite de Cumplimiento:** 7 mayo del 2026  

---

## 🎯 Objetivo del Proyecto

Desarrollar un aplicativo web funcional que permita a un usuario autenticado gestionar tareas de manera organizada, con persistencia de información y apoyo de inteligencia artificial, demostrando dominio de los resultados de aprendizaje:

- **CREAR COMPONENTES FRONT-END DEL SOFTWARE DE ACUERDO CON EL DISEÑO**
- **CARACTERIZAR LOS PROCESOS DE LA ORGANIZACIÓN DE ACUERDO CON EL SOFTWARE A CONSTRUIR**
- **VALIDAR EL INFORME DE REQUISITOS DE ACUERDO CON LAS NECESIDADES DEL CLIENTE**
- **VERIFICAR LOS ENTREGABLES DE LA FASE DE DISEÑO DEL SOFTWARE DE ACUERDO CON LO ESTABLECIDO EN EL INFORME DE ANÁLISIS**

---

## 📋 Descripción del Aplicativo

El **Asistente de Tareas SENA** es una aplicación web que permite:

✅ **Autenticación segura** con Firebase Authentication (Google OAuth)  
✅ **Acceso restringido** mediante guards para rutas privadas  
✅ **Registro de información** (tareas, mensajes, consultas)  
✅ **Visualización de datos** almacenados previamente  
✅ **Interacción con IA** para sugerencias y apoyo (Gemini API)  
✅ **Persistencia de datos** en Firestore  
✅ **Recuperación automática** de información al reingresar  
✅ **Cierre de sesión** seguro  

### Flujo de Funcionamiento
1. **Inicio:** Pantalla de autenticación
2. **Validación:** Firebase verifica credenciales
3. **Acceso:** Redirección a zona privada (protegida por guard)
4. **Interacción:** Usuario registra tareas y consulta IA
5. **Persistencia:** Datos se guardan en Firestore
6. **Reingreso:** Información se recupera automáticamente

---

## 🏗️ Arquitectura del Proyecto

### Estructura de Carpetas
```
src/
├── app/
│   ├── components/
│   │   ├── auth/          # Componente de autenticación
│   │   └── chat/          # Componente principal (asistente de tareas)
│   ├── services/          # Servicios de negocio
│   │   ├── auth.ts        # Autenticación con Firebase
│   │   ├── chat.ts        # Gestión de mensajes/tareas
│   │   ├── firebase.ts    # Conexión a Firestore
│   │   └── gemini.ts      # Integración con IA
│   ├── guards/            # Protección de rutas
│   │   └── auth-guard.ts  # Guard para rutas privadas
│   ├── models/            # Interfaces TypeScript
│   │   ├── chat.ts        # Modelo de mensajes
│   │   └── usuario.ts     # Modelo de usuario
│   ├── app.config.ts      # Configuración central
│   ├── app.routes.ts      # Definición de rutas
│   └── app.ts             # Componente raíz
├── environments/          # Variables de entorno
└── main.ts               # Punto de entrada
```

### Diagrama de Arquitectura
```
┌─────────────────────────────────────────┐
│         Angular Application            │
│              Router Outlet             │
└─────────────────────────────────────────┘
              ↓
    ┌─────────┴──────────┐
    ↓                    ↓
┌─────────┐      ┌──────────────┐
│  Auth   │      │  Task Asst   │
│Component│      │ Component    │
└────┬────┘      └──────┬───────┘
     │                  │
     └──────────┬───────┘
                ↓
      ┌─────────────────────┐
      │   SERVICIOS (DI)    │
      └─────────────────────┘
              ↙ ↓ ↘
      ┌────┐ ┌────┐ ┌────┐
      │Auth│ │Task│ │Fire│
      │Svc │ │Svc │ │Svc │
      └────┘ └────┘ └────┘
        ↓       ↓       ↓
    Google   Gemini Firestore
    OAuth    API     DB
```

---

## 🚀 Tecnologías Utilizadas

### **Angular 19**
- **Framework frontend** con componentes standalone
- **Routing** con lazy loading
- **Inyección de dependencias** para servicios
- **Forms** para manejo de inputs

### **Firebase**
- **Authentication:** Login seguro con Google
- **Firestore:** Base de datos NoSQL en tiempo real
- **Hosting:** Despliegue de la aplicación

### **Google Gemini API**
- **Servicio de IA** para respuestas inteligentes
- **Integración REST** vía HttpClient
- **Procesamiento de lenguaje natural**

### **TypeScript**
- **Tipado estático** para modelos de datos
- **Interfaces** para Usuario, MensajeChat, etc.

### **RxJS**
- **Observables** para manejo de datos asíncronos
- **BehaviorSubject** para estado reactivo

---

## 📦 Instalación y Configuración

### Prerrequisitos
- Node.js 18+
- npm o yarn
- Cuenta de Google (para Firebase)
- API Key de Gemini

### Instalación
```bash
# Clonar repositorio
git clone <url-del-repositorio>
cd asistente-tareas-sena

# Instalar dependencias
npm install

# Instalar Angular CLI globalmente (si no está)
npm install -g @angular/cli
```

### Configuración de Firebase
1. Crear proyecto en [Firebase Console](https://console.firebase.google.com)
2. Habilitar Authentication con Google
3. Crear base de datos Firestore
4. Obtener configuración y API keys

### Variables de Entorno
Crear `src/environments/environment.ts`:
```typescript
export const environment = {
  production: false,
  firebaseConfig: {
    apiKey: "your-api-key",
    authDomain: "your-project.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "your-app-id"
  },
  gemini: {
    apiKey: "your-gemini-api-key"
  }
};
```

### Configuración de Gemini API
1. Obtener API key de [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Agregar al environment.ts

---

## 🎮 Uso del Aplicativo

### Inicio de Sesión
1. Acceder a la URL del aplicativo
2. Hacer clic en "Iniciar sesión con Google"
3. Autorizar permisos en popup
4. Redirección automática a zona privada

### Gestión de Tareas
1. **Agregar tarea:** Escribir en el campo de texto y enviar
2. **Marcar completada:** Checkbox junto a cada tarea
3. **Eliminar tarea:** Botón "Eliminar" en cada tarea
4. **Consultar IA:** Enviar mensaje para obtener ayuda

### Cierre de Sesión
- Botón "Salir" en la esquina superior derecha
- Redirección a pantalla de login

---

## 🌐 Despliegue

### Despliegue Local
```bash
# Desarrollo
npm start
# Acceder en http://localhost:4200

# Producción local
npm run build
npm run serve
```

### Despliegue en Firebase
```bash
# Instalar Firebase CLI
npm install -g firebase-tools

# Login y configuración
firebase login
firebase init hosting

# Desplegar
npm run build
firebase deploy

https://asistenteia-f4efd.web.app/chat
```

### Verificación de Despliegue
- ✅ Aplicación carga correctamente
- ✅ Autenticación funciona
- ✅ Datos se persisten
- ✅ IA responde
- ✅ Responsive en móviles

---

## 📚 Documentación Técnica

### Componentes Principales

#### **AuthComponent** (`src/app/components/auth/`)
- **Propósito:** Interfaz de autenticación
- **Funciones:**
  - `iniciarSesionConGoogle()`: Inicia flujo OAuth
  - Manejo de errores de autenticación
- **Dependencias:** AuthService, Router

#### **ChatComponent** (`src/app/components/chat/`)
- **Propósito:** Interfaz principal del asistente
- **Funciones:**
  - `enviarMensaje()`: Envía consulta a IA
  - `agregarTarea()`: Agrega nueva tarea
  - `toggleTarea()`: Marca tarea completada
  - `eliminarTarea()`: Elimina tarea
- **Dependencias:** ChatService, AuthService

### Servicios

#### **AuthService** (`src/app/services/auth.ts`)
- **Métodos principales:**
  - `iniciarSesionConGoogle()`: Autenticación OAuth
  - `cerrarSesion()`: Logout
  - `obtenerUsuarioActual()`: Usuario actual

#### **ChatService** (`src/app/services/chat.ts`)
- **Métodos principales:**
  - `inicializarChat()`: Carga historial
  - `enviarMensaje()`: Envía a Gemini y guarda
  - `limpiarChat()`: Limpia estado

#### **FirebaseService** (`src/app/services/firebase.ts`)
- **Métodos principales:**
  - `guardarMensaje()`: Persiste mensaje
  - `obtenerMensajesUsuario()`: Recupera historial

#### **GeminiService** (`src/app/services/gemini.ts`)
- **Métodos principales:**
  - `enviarMensaje()`: Consulta a API
  - `convertirHistorialGemini()`: Formatea datos

### Guards

#### **AuthGuard** (`src/app/guards/auth-guard.ts`)
- **Propósito:** Protege rutas privadas
- **Lógica:** Verifica usuario autenticado, redirige si no

### Modelos de Datos

#### **Usuario** (`src/models/usuario.ts`)
```typescript
export interface Usuario {
  uid: string;
  email: string;
  nombre: string;
  fotoUrl?: string;
  fechaCreacion: Date;
  ultimaConexion: Date;
}
```

#### **MensajeChat** (`src/models/chat.ts`)
```typescript
export interface MensajeChat {
  id?: string;
  fechaEnvio: Date;
  contenido: string;
  usuarioId: string;
  tipo: "usuario" | "asistente";
  estado?: "enviado" | "error";
}
```

---

## 🔍 Análisis de Requisitos

### Requisitos Funcionales Cumplidos

| Requisito | Implementación | Archivo |
|-----------|---------------|---------|
| Autenticación de usuario | Firebase Auth + Google OAuth | `auth.ts`, `auth.html` |
| Acceso restringido | AuthGuard en rutas | `auth-guard.ts`, `app.routes.ts` |
| Registro de información | Formulario de tareas + chat | `chat.html`, `chat.ts` |
| Interacción con IA | Gemini API integration | `gemini.ts`, `chat.ts` |
| Persistencia de datos | Firestore para mensajes/tareas | `firebase.ts` |
| Recuperación de información | Carga automática al login | `chat.ts` |
| Cierre de sesión | Logout seguro | `auth.ts` |

### Arquitectura Técnica

- **Separación de responsabilidades:** Componentes, servicios, guards
- **Inyección de dependencias:** Servicios compartidos
- **Lazy loading:** Componentes cargados bajo demanda
- **Reactive programming:** RxJS para manejo de estado
- **Type safety:** TypeScript interfaces

---

## 🎓 Reflexión Individual

Como aprendiz del Programa Tecnólogo en Análisis y Desarrollo de Software, este proyecto me permitió demostrar comprensión profunda de los conceptos trabajados durante el trimestre:

### Aprendizajes Técnicos
- **Angular Framework:** Desarrollo con componentes standalone, routing, guards
- **Firebase Ecosystem:** Autenticación, base de datos en tiempo real, hosting
- **APIs Externas:** Integración con servicios de IA (Gemini)
- **Arquitectura de Software:** Separación de capas, inyección de dependencias
- **TypeScript:** Tipado estático, interfaces, clases

### Desafíos Encontrados
- Configuración inicial de Firebase y Gemini
- Manejo de observables y suscripciones RxJS
- Protección de rutas con guards
- Persistencia y sincronización de datos

### Soluciones Implementadas
- Investigación en documentación oficial
- Pruebas iterativas de componentes
- Debugging con herramientas de desarrollo
- Optimización de rendimiento

### Resultados de Aprendizaje Demostrados
- ✅ Creación de componentes front-end coherentes con el diseño
- ✅ Caracterización de procesos organizacionales en el software
- ✅ Validación de requisitos según necesidades del cliente
- ✅ Verificación de entregables de diseño

Este aplicativo no solo cumple con los requisitos técnicos, sino que demuestra capacidad para desarrollar soluciones completas de software, desde la concepción hasta el despliegue funcional.

---

## 📞 Contacto

**Desarrollado por:** Juan Jose Bocanegra  
**Instructor:** Yennifer Steffi Velandia Soto  
**Centro:** Centro de Biotecnología Agropecuario SENA  
**Fecha:** Mayo 2026

---

*Este proyecto es evidencia del cumplimiento del Plan de Mejoramiento Académico y demuestra apropiación técnica de los resultados de aprendizaje del trimestre.*
'@
