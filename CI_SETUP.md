# Configuración CI/CD para VetSync

## 🚀 Pipeline Configurado

He configurado un pipeline completo de CI/CD usando GitHub Actions con los siguientes workflows:

### 1. **CI/CD Pipeline** (`.github/workflows/ci.yml`)
- **Trigger:** Push a main/develop, Pull Requests a main
- **Jobs:**
  - **Test:** Ejecuta en Node.js 18.x y 20.x
    - ESLint (calidad de código)
    - Security audit (vulnerabilidades)
    - Build (compilación)
  - **Deploy:** Solo en push a main
    - Build y deploy automático a Vercel

### 2. **Code Quality** (`.github/workflows/code-quality.yml`)
- **Trigger:** Pull Requests a main
- **Features:**
  - ESLint con anotaciones en GitHub
  - Verificación de tamaño de bundle
  - Revisión de dependencias

### 3. **Security Scan** (`.github/workflows/security.yml`)
- **Trigger:** Daily, push a main, Pull Requests
- **Features:**
  - npm audit completo
  - Snyk security scan (opcional)

## 🔧 Configuración Requerida

### Variables de Entorno en GitHub
Ve a `Settings > Secrets and variables > Actions` y agrega:

```
VERCEL_TOKEN=token_de_vercel
VERCEL_ORG_ID=id_de_organizacion_vercel
VERCEL_PROJECT_ID=id_de_proyecto_vercel
SNYK_TOKEN=token_de_snyk (opcional)
```

### Obtener Tokens de Vercel
1. Instala Vercel CLI: `npm i -g vercel`
2. Login: `vercel login`
3. Link project: `vercel link`
4. Obtén IDs: `vercel env ls`

## 📋 Comandos Locales

```bash
# Ejecutar todas las pruebas de CI localmente
npm run test:ci

# Linting
npm run lint

# Build
npm run build

# Security audit
npm audit --audit-level=moderate
```

## 🔄 Flujo de Trabajo

1. **Developer** crea feature branch
2. **Push** trigger: Tests en Node 18.x y 20.x
3. **Pull Request**: Code quality checks
4. **Merge a main**: Deploy automático a producción

## ✅ Beneficios

- **Calidad garantizada:** Código validado antes de merge
- **Seguridad:** Detección automática de vulnerabilidades
- **Despliegue seguro:** Solo código probado va a producción
- **Multi-version:** Compatible con Node.js 18.x y 20.x
- **Monitoreo:** Scans de seguridad diarios

## 🚀 Primer Uso

1. Commit y push los archivos `.github/workflows/`
2. Configura los secrets en GitHub
3. Crea un pull request para probar el pipeline
4. Merge a main para activar deploy automático
