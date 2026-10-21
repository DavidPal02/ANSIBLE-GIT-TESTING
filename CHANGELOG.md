# Changelog

Todos los cambios relevantes de este proyecto se documentan en este fichero.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/),
y este proyecto se adhiere al [Semantic Versioning](https://semver.org/lang/es/).

## [0.1.0] - 2026-10-21

### Añadido
- Estructura inicial del proyecto "La compra de la familia".
- Tres roles Ansible: `verduras_frutas`, `carne_pescado`, `lacteos_galletas`.
- Playbook principal `site.yml` con `import_role` para los tres roles.
- Documentación por rol: `README.md`, `INSTRUCCIONES.md`, `SOLUCION.md`.
- Inventario local (`localhost ansible_connection=local`).
- Configuración de CI con `.travis.yml`.
- Rama `dev/david` (bebidas y refrescos) añadida e integrada en `main`.
