# ElectronApp

Aplicación de escritorio construida con Angular y Electron.

## Tabla de Contenidos
- [Configuración Inicial](#configuración-inicial)
- [Modos de Ejecución](#modos-de-ejecución)
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Comandos Disponibles](#comandos-disponibles)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Configuración de Desarrollo](#configuración-de-desarrollo)
- [Construcción y Despliegue](#construcción-y-despliegue)
- [Solución de Problemas](#solución-de-problemas-comunes)
- [Contribución](#contribución)
- [Recursos Adicionales](#recursos-adicionales)

## Requisitos Previos
- Node.js (versión 18 o superior)
- npm (incluido con Node.js)
- Angular CLI (`npm install -g @angular/cli`)
- Git (para control de versiones)

## Instalación

1. Clonar el repositorio:
```bash
git clone <url-del-repositorio>
cd electronApp
```

2. Instalar dependencias:
```bash
npm install
```

3. Verificar la instalación:
```bash
npm run electron:dev
```

## Modos de Ejecución

### Modo Desarrollo

#### Aplicación Web (Solo Angular)
```bash
ng serve
```
Navega a `http://localhost:4200/`. La aplicación se recargará automáticamente si cambias algún archivo.

#### Aplicación de Escritorio con Hot Reload
```bash
npm run electron:dev
```
Este comando:
- Inicia el servidor de desarrollo de Angular
- Abre la aplicación en Electron
- Actualiza automáticamente al hacer cambios

### Modo Producción

#### Compilar y Probar Localmente
```bash
npm run electron:local
```
Compila y ejecuta la versión de producción localmente.

#### Crear Ejecutable Distribuible
```bash
npm run electron:dist
```
Genera el instalador en la carpeta `release/`:
- Windows: archivo .exe
- macOS: archivo .dmg
- Linux: archivo .AppImage

## Configuración de Desarrollo

### Estructura de Archivos Principales
```
src/
├── app/
│   ├── app.component.ts    # Componente principal
│   ├── app.component.html  # Template principal
│   └── app.routes.ts       # Configuración de rutas
├── electron/
│   └── main.ts            # Punto de entrada de Electron
└── index.html             # HTML principal
```

### Archivos de Configuración
- `electron-builder.json`: Configuración para crear instaladores
- `package.json`: Scripts y dependencias
- `tsconfig.json`: Configuración de TypeScript
- `angular.json`: Configuración de Angular

## Construcción y Despliegue

### Proceso de Construcción
1. Compilar Angular:
```bash
ng build --prod
```

2. Compilar Electron:
```bash
tsc src/electron/main.ts --outDir dist/electron
```

3. Crear instalador:
```bash
npm run electron:dist
```

### Configuración de Electron Builder
```json
{
  "productName": "ElectronApp",
  "directories": {
    "output": "release/"
  },
  "files": [
    "dist/**/*",
    "package.json"
  ]
}
```

## Características Principales
- 🔄 Hot Reload en desarrollo
- 🖥️ Interfaz de escritorio nativa
- 📦 Generación de instaladores
- 🛠️ DevTools integradas
- 🚀 Optimización de producción

## Solución de Problemas Comunes

### Error: Cannot find module 'electron'
Solución: Reinstalar las dependencias de Electron
```bash
npm install --save-dev electron electron-builder @types/electron
```

### Error: Failed to load URL
Solución: Verificar que el `base href` en index.html sea:
```html
<base href="./">
```

### Error: App no se actualiza en desarrollo
Solución: Reiniciar el comando de desarrollo
```bash
npm run electron:dev
```

### Error: node_modules no encontrado
Solución: Limpiar caché e instalar
```bash
rm -rf node_modules
npm cache clean --force
npm install
```

## Contribución
1. Fork el proyecto
2. Crea tu rama de característica (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## Scripts Personalizados
```json
{
  "scripts": {
    "electron:dev": "concurrently \"ng serve\" \"wait-on http://localhost:4200 && electron . --serve\"",
    "electron:build": "ng build --base-href ./ && tsc src/electron/main.ts --outDir dist/electron",
    "electron:local": "npm run electron:build && electron .",
    "electron:dist": "electron-builder -c electron-builder.json"
  }
}
```

## Versiones Compatibles
- Angular: ^19.1.0
- Electron: ^28.0.0
- Node.js: >=18.0.0
- TypeScript: ~5.7.2

## Recursos Adicionales
- [Angular Documentation](https://angular.dev/)
- [Electron Documentation](https://www.electronjs.org/docs/latest/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Electron Builder Documentation](https://www.electron.build/)

## Licencia
Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE.md](LICENSE.md) para detalles

## Contacto
Nombre - [@twitter_handle](https://twitter.com/twitter_handle)
Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)

## Comandos Disponibles

| Comando | Descripción |
|---------|-------------|
| `npm run electron:dev` | Desarrollo con hot reload |
| `npm run electron:local` | Ejecutar versión compilada |
| `npm run electron:dist` | Crear instalador |
| `npm run electron:build` | Solo compilar |
| `ng serve` | Servidor de desarrollo Angular |
| `ng build` | Compilar proyecto Angular |
| `ng test` | Ejecutar tests unitarios |
| `ng generate component nombre` | Generar nuevo componente |

## Estructura del Proyecto

```
├── src/
│   ├── app/                 # Código fuente Angular
│   ├── electron/           # Código fuente Electron
│   │   └── main.ts         # Punto de entrada Electron
│   └── assets/            # Recursos estáticos
├── dist/                  # Archivos compilados
└── release/              # Instaladores generados
```

## Notas de Desarrollo
- Los cambios en archivos Angular se recargan automáticamente en modo desarrollo
- Las DevTools de Electron están disponibles en modo desarrollo
- La aplicación se inicia maximizada por defecto
