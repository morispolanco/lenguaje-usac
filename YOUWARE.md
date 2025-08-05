# Lenguaje USAC - Plataforma Educativa

Esta aplicación educativa está diseñada para la preparación del examen de lenguaje de la Universidad de San Carlos de Guatemala, basada en la Guía Temática oficial.

## Información del Proyecto

- **Tipo**: Aplicación web educativa completa
- **Punto de entrada**: `index.html`
- **Tecnologías**: HTML5, CSS3, JavaScript Vanilla, Supabase, Stripe, Gemini AI
- **Audiencia**: Jóvenes estudiantes que se preparan para ingresar a la USAC

## Arquitectura del Sistema

### Backend (Supabase)
- **Proyecto activo**: "Lenguaje" (ID: augrzzbvroycxdosamom)
- **Estado**: ACTIVE_HEALTHY
- **Región**: us-east-1
- **URL**: https://augrzzbvroycxdosamom.supabase.co

### Estructura de Base de Datos

```sql
-- Perfiles de usuario extendidos
profiles (
    id uuid PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id),
    email text NOT NULL,
    first_name text,
    last_name text,
    created_at timestamptz DEFAULT now(),
    updated_at timestamptz DEFAULT now()
)

-- Módulos educativos (6 módulos principales)
modules (
    id uuid PRIMARY KEY,
    title text NOT NULL,
    description text,
    order_index integer NOT NULL,
    created_at timestamptz DEFAULT now()
)

-- Unidades/lecciones dentro de cada módulo
units (
    id uuid PRIMARY KEY,
    module_id uuid REFERENCES modules(id),
    title text NOT NULL,
    description text,
    content text,
    order_index integer NOT NULL,
    created_at timestamptz DEFAULT now()
)

-- Progreso del usuario por unidad
user_progress (
    id uuid PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id),
    unit_id uuid REFERENCES units(id),
    completed boolean DEFAULT false,
    completed_at timestamptz,
    created_at timestamptz DEFAULT now()
)

-- Resultados de quizzes
quiz_results (
    id uuid PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id),
    unit_id uuid REFERENCES units(id),
    score integer CHECK (score >= 0 AND score <= 100),
    total_questions integer NOT NULL,
    correct_answers integer NOT NULL,
    created_at timestamptz DEFAULT now()
)
```

## Módulos Educativos

La aplicación incluye 6 módulos principales basados en la Guía Temática oficial:

1. **Comunicación** - Elementos, funciones del lenguaje, argumentación
2. **Lenguaje** - Signo lingüístico, tipos, disciplinas  
3. **Ortografía** - Reglas, acentuación, puntuación
4. **Gramática y Vocabulario** - Análisis, categorías, formación
5. **Exposición Oral y Escrita** - Redacción, tipos de texto
6. **Comprensión Lectora** - Estrategias, figuras literarias

## Integraciones Configuradas

### Supabase (Habilitado)
- **Autenticación**: Sistema completo de registro/login
- **Base de datos**: Almacenamiento de progreso y contenido
- **RLS**: Políticas de seguridad a nivel de fila habilitadas

### Stripe (Configurado)
- **Clave pública**: pk_live_51JOLcwFlSFoL2Zh4SekRb1wkEsJTmKFycTZo7uxBmJ2FhclabFO7gbZp1q3WMsk7mNXqrPIti4dIoSXfNyosxSbO00k1QZ3GaN
- **Precio**: price_1RsCvfFlSFoL2Zh44D5nxCpx ($19 USD)
- **Tipo**: Pago único, licencia de por vida

### Gemini AI (Integrado)
- **API Key**: AIzaSyAzM-0NsO1tLMu6RHpQJSPBXUbJ0PjRj8E
- **Modelos Implementados**: 
  - gemini-2.5-pro: Para generación de contenido extenso y rutas de aprendizaje
  - gemini-2.5-flash: Para respuestas rápidas del asistente
- **Escenarios de uso**:
  - Generación de lecciones educativas
  - Creación de quizzes personalizados
  - Asistente de dudas para estudiantes
  - Rutas de aprendizaje adaptativas

## Funcionalidades Principales

### Sistema de Autenticación
- Registro de usuarios con validación
- Login seguro con Supabase Auth
- Perfiles de usuario persistentes
- Gestión de sesiones automática

### Sistema de Progreso
- Seguimiento por módulo y unidad
- Puntuación basada en completitud y quiz results
- Sistema de insignias (1 por cada 100 puntos)
- Barras de progreso visuales

### Sistema de Gamificación
- Puntos por lecciones completadas
- Resultados de quizzes almacenados
- Estadísticas de progreso en tiempo real
- Insignias por logros

### Gestión de Contenido
- Contenido estructurado por módulos
- Lecciones organizadas secuencialmente
- Quizzes interactivos por módulo
- Poblamiento automático de datos base

## Estado de Desarrollo

### ✅ Completado
- Estructura base HTML/CSS/JS
- Sistema de autenticación con Supabase
- Base de datos configurada y poblada
- Sistema de progreso y gamificación
- Interfaz de usuario responsive
- Generación de contenido con Gemini AI
- Sistema de quizzes con IA
- Asistente virtual para estudiantes
- Rutas de aprendizaje personalizadas
- Integración completa de pagos con Stripe
- Configuración para despliegue en Vercel

### 🔄 Pendiente
- Completar contenido de todos los módulos
- Tests automatizados
- Optimizaciones de rendimiento

## Comandos y Desarrollo

### Desarrollo Local
```bash
# Servidor web simple para desarrollo
npm run serve

# Servidor de desarrollo Vercel (con variables de entorno)
npm run dev

# Abrir directamente en navegador (para desarrollo básico)
open index.html
```

### Despliegue
```bash
# Vista previa de despliegue
npm run preview

# Despliegue a producción
npm run deploy
```

### Estructura de Archivos
- `index.html` - Punto de entrada principal
- `app.js` - Lógica de aplicación y gestión de estado
- `styles.css` - Estilos CSS responsivos
- `yw_manifest.json` - Configuración de modelos IA
- `vercel.json` - Configuración de despliegue y variables
- `package.json` - Scripts y dependencias del proyecto

### Variables de Entorno para Vercel
```
SUPABASE_URL=https://augrzzbvroycxdosamom.supabase.co
SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImF1Z3J6emJ2cm95Y3hkb3NhbW9tIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTQyODgxNTEsImV4cCI6MjA2OTg2NDE1MX0.QvZkp8c-zAioBX1VjBOzHVLh4BZtXNTgbiz6UfuNbKY
STRIPE_PUBLISHABLE_KEY=pk_live_51JOLcwFlSFoL2Zh4SekRb1wkEsJTmKFycTZo7uxBmJ2FhclabFO7gbZp1q3WMsk7mNXqrPIti4dIoSXfNyosxSbO00k1QZ3GaN
STRIPE_SECRET_KEY=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
STRIPE_PRICE_ID=price_1RsCvfFlSFoL2Zh44D5nxCpx
GEMINI_API_KEY=AIzaSyAzM-0NsO1tLMu6RHpQJSPBXUbJ0PjRj8E
```

## Funciones JavaScript Principales

### Autenticación
- `supabaseAuth.signUp(email, password)` - Registro de usuarios
- `supabaseAuth.signIn(email, password)` - Inicio de sesión
- `supabaseAuth.signOut()` - Cierre de sesión
- `loadUserProfile()` - Carga perfil y progreso del usuario

### Gestión de Progreso
- `saveUserProgress(moduleId, unitId, completed)` - Guarda progreso
- `saveQuizResult(unitId, score, total, correct)` - Guarda resultados de quiz
- `updateUserStats()` - Actualiza estadísticas de usuario

### Contenido
- `loadModulesData()` - Carga módulos desde base de datos
- `populateDefaultModules()` - Crea módulos por defecto
- `generateLessonContent(title, moduleId)` - Genera contenido con Gemini AI
- `generateQuizData(moduleId)` - Genera quizzes con IA estructurados
- `askAI(question, topic, concept)` - Asistente IA para estudiantes
- `resetAIConversation()` - Reinicia historial de conversación IA
- `generateLearningPath(moduleId, level, strengths, weaknesses)` - Genera rutas de aprendizaje

## Consideraciones de Seguridad

- RLS (Row Level Security) habilitado en todas las tablas
- Validación de entrada en frontend y backend
- Autenticación basada en JWT con Supabase
- Claves API configuradas como variables de entorno

## Próximos Pasos de Desarrollo

1. Completar integración de pagos con Stripe
2. Implementar generación de contenido con Gemini AI
3. Añadir más contenido educativo detallado
4. Optimizar para despliegue en Vercel
5. Implementar tests automatizados