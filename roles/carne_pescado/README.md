# Rol: carne_pescado

Rol educativo que simula la sección de **carne y pescado** de la compra
familiar. Responsable: **Moisés**.

Crea una carpeta `/tmp/compras/moises/carne_pescado/` con un archivo por
producto comprado.

## Variables por defecto

Definidas en `defaults/main.yml`:

| Variable | Valor |
|---|---|
| `seccion_persona` | `Moisés` |
| `seccion_nombre` | `Carne y pescado` |

## Cómo ejecutarlo

```bash
ansible-playbook -i inventory-site.yml site.yml
```

## Documentación

- [INSTRUCCIONES.md](INSTRUCCIONES.md) — pistas bash para construirlo.
- [SOLUCION.md](SOLUCION.md) — versión final lista para revisar.
