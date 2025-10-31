# Configuración de GitHub Actions - Lab PDS U2-02

## Variables Secretas Requeridas

Para que los workflows funcionen correctamente, debes configurar las siguientes variables secretas en tu repositorio de GitHub:

### Pasos para configurar secrets:

1. Ve a tu repositorio en GitHub
2. Navega a **Settings** → **Secrets and variables** → **Actions**
3. Haz clic en **New repository secret**
4. Configura los siguientes secrets:

### Secrets Necesarios:

#### `SONAR_TOKEN`
- **Descripción**: Token para análisis con SonarCloud
- **Obtener en**: https://sonarcloud.io/account/security
- **Organización SonarCloud**: `sebastianfuentesavalos`
- **Project Key**: `sebastianfuentesavalos_lab-2025-ii-pds-u2-02-nest-sebastianfuentesavalos`

#### `NUGET_API_KEY` (usado para GitHub Packages)
- **Descripción**: Personal Access Token para publicar paquetes NPM en GitHub Packages
- **Obtener en**: GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
- **Permisos necesarios**:
  - `write:packages`
  - `read:packages`
  - `delete:packages`

### Configuración de SonarCloud

1. Ve a https://sonarcloud.io/
2. Inicia sesión con tu cuenta de GitHub
3. Crea una nueva organización:
   - **Organization**: `sebastianfuentesavalos`
   - **Display Name**: `lab-2025-ii-pds-u2-02-nest-SebastianFuentesAvalos`
   - **Project Key**: `sebastianfuentesavalos_lab-2025-ii-pds-u2-02-nest-sebastianfuentesavalos`

### Configuración de GitHub Pages

1. Ve a **Settings** → **Pages**
2. En **Source** selecciona **GitHub Actions**
3. Los workflows publicarán automáticamente la documentación

## Workflows Disponibles

### 1. `publish_docs.yml`
- **Trigger**: Push a main, PR, manual
- **Función**: Genera documentación con Compodoc y publica en GitHub Pages
- **Salida**: Documentación accesible en GitHub Pages

### 2. `package_npm.yml` 
- **Trigger**: Push a main/develop, PR, manual
- **Función**: 
  - Ejecuta pruebas unitarias
  - Análisis con SonarCloud
  - Publica paquetes en GitHub Packages
- **Paquetes**: 
  - `@sebastianfuentesavalos/notifications_fuentesavalos`
  - `@sebastianfuentesavalos/customer-app_fuentesavalos`

### 3. `release_version.yml`
- **Trigger**: Tags `v*`, manual con input de versión
- **Función**: 
  - Crea releases en GitHub
  - Genera archivos comprimidos
  - Publica changelog automático

## Uso de los Workflows

### Para crear un release:

#### Opción 1: Manual con versión
1. Ve a **Actions** → **Create Release Version**
2. Haz clic en **Run workflow**
3. Ingresa la versión (ej: `1.0.0`)

#### Opción 2: Con tag
```bash
git tag v1.0.0
git push origin v1.0.0
```

### Para forzar publicación de documentación:
1. Ve a **Actions** → **Publish Documentation**
2. Haz clic en **Run workflow**

## Estructura de Paquetes

Los paquetes publicados tendrán la siguiente estructura:
- `notifications_fuentesavalos` - Implementación del patrón Bridge
- `customer-app_fuentesavalos` - Implementación del patrón Facade

## Instalación de Paquetes

```bash
# Notifications package
npm install @sebastianfuentesavalos/notifications_fuentesavalos

# Customer App package  
npm install @sebastianfuentesavalos/customer-app_fuentesavalos
```

---

**Autor**: Sebastian Fuentes Avalos  
**Curso**: Patrones de Diseño de Software - UPT  
**Laboratorio**: PDS U2-02 - Patrones Estructurales