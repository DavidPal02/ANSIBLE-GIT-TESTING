# Rol: verduras_frutas

Rol educativo que simula la sección de **verduras y frutas** de la compra
familiar. Responsable: **Ricardo**.

Crea una carpeta `/tmp/compras/ricardo/verduras_frutas/` con un archivo por
producto comprado.

## Variables por defecto

Definidas en `defaults/main.yml`:

| Variable | Valor |
|---|---|
| `seccion_persona` | `Ricardo` |
| `seccion_nombre` | `Verduras y frutas` |

(Los productos también están como variables, pero las tareas los imprimen en
el comando para mantener la implementación tipo bash.)

## Cómo ejecutarlo

```bash
ansible-playbook -i inventory-site.yml site.yml
```

## Documentación

- [INSTRUCCIONES.md](INSTRUCCIONES.md) — pistas bash para construirlo.
- [SOLUCION.md](SOLUCION.md) — versión final lista para revisar.
