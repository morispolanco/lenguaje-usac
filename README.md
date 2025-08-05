# Lenguaje USAC - Plataforma Educativa

Plataforma educativa para preparación del examen de lenguaje de la Universidad de San Carlos de Guatemala.

## 📋 Descripción

Esta aplicación web educativa está diseñada para ayudar a estudiantes a prepararse para el examen de lenguaje de la USAC, basada en la Guía Temática oficial. La plataforma ofrece contenido educativo, quizzes interactivos y un asistente virtual potenciado por IA.

## ✨ Características Principales

- 🔐 **Sistema de Autenticación**: Registro y login seguros con Supabase Auth
- 📚 **6 Módulos Educativos**: Contenido estructurado según la Guía Temática oficial
- 🧠 **IA Generativa**: Contenido personalizado y asistente virtual con Google Gemini
- 🎮 **Sistema de Gamificación**: Puntos, insignias y progreso visual
- 💰 **Pagos Integrados**: Sistema de pago único con Stripe
- 📱 **Diseño Responsive**: Adaptado a todos los dispositivos

## 🚀 Despliegue

### Requisitos Previos

- Cuenta en Vercel
- Cuenta en Supabase con proyecto configurado
- Cuenta en Stripe con producto y precio configurados
- API Key de Google Gemini

### Configuración de URLs de Auth en Supabase

⚠️ **IMPORTANTE**: Para solucionar el problema de redirección a localhost en emails de confirmación:

1. Ve al Dashboard de Supabase: https://supabase.com/dashboard/project/augrzzbvroycxdosamom
2. Navega a **Authentication > URL Configuration**
3. Configura las siguientes URLs:

   **Site URL (URL principal):**
   ```
   https://lenguaje-usac.vercel.app
   ```

   **Additional Redirect URLs (URLs adicionales permitidas):**
   ```
   https://lenguaje-usac.vercel.app/**
   http://localhost:3000/**
   ```

4. Guarda los cambios

### Pasos para Desplegar

1. **Clonar el repositorio**

```bash
git clone https://github.com/tu-usuario/lenguaje-usac.git
cd lenguaje-usac
```

2. **Instalar dependencias**

```bash
npm install
```

3. **Configurar variables de entorno en Supabase Edge Functions**

```bash
# Configurar variables para Edge Functions
npx supabase secrets set --project-ref augrzzbvroycxdosamom \
  STRIPE_SECRET_KEY=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 \
  STRIPE_PRICE_ID=price_1RsCvfFlSFoL2Zh44D5nxCpx \
  APP_URL=https://lenguaje-usac.vercel.app \
  SUPABASE_URL=https://augrzzbvroycxdosamom.supabase.co \
  SUPABASE_SERVICE_ROLE_KEY=tu_service_role_key \
  STRIPE_WEBHOOK_SECRET=tu_webhook_secret_de_stripe
```

4. **Configurar webhook en Stripe**

- Ve al Dashboard de Stripe > Desarrolladores > Webhooks
- Añade un nuevo endpoint: `https://augrzzbvroycxdosamom.functions.supabase.co/stripe-webhook`
- Selecciona los eventos: `checkout.session.completed`
- Guarda el Signing Secret generado para usarlo como `STRIPE_WEBHOOK_SECRET`

5. **Desplegar en Vercel**

```bash
npm run deploy
```

También puedes conectar tu repositorio a Vercel para despliegues automáticos:

- Importa tu repositorio en Vercel
- Configura las variables de entorno según las definidas en `vercel.json`
- Despliega la aplicación

## 🛠️ Desarrollo Local

```bash
# Servidor de desarrollo con variables de entorno
npm run dev

# Servidor simple para desarrollo básico
npm run serve

# Vista previa de despliegue
npm run preview
```

## 📊 Estructura del Proyecto

- `index.html`: Punto de entrada principal
- `app.js`: Lógica de la aplicación y gestión de estado
- `styles.css`: Estilos CSS responsivos
- `vercel.json`: Configuración de despliegue
- `package.json`: Scripts y dependencias del proyecto
- `yw_manifest.json`: Configuración de modelos IA

## 🔒 Seguridad

La aplicación implementa:

- Row Level Security (RLS) en Supabase
- Autenticación basada en JWT
- Content Security Policy (CSP) en producción
- Validación de entrada en frontend y backend
- Claves API protegidas con variables de entorno

## 📝 Licencia

Este proyecto está licenciado bajo la Licencia MIT - vea el archivo LICENSE para más detalles.

---

Desarrollado por el equipo de Lenguaje USAC