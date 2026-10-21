# Rol: bebidas_refrescos

Rol educativo que simula la sección de **bebidas y refrescos** de la compra
familiar. Responsable: **David**.

## Variables por defecto

| Variable | Valor |
|---|---|
| `seccion_persona` | `David` |
| `seccion_nombre` | `Bebidas y refrescos` |
| `bebidas_agua` | `Agua mineral 1.5L` |
| `bebidas_zumo_naranja` | `Zumo de naranja natural` |
| `bebidas_zumo_manzana` | `Zumo de manzana` |
| `refrescos_cola` | `Refresco de cola` |
| `refrescos_limon` | `Refresco de limón` |
| `refrescos_naranja` | `Refresco de naranja` |
| `cerveza` | `Cerveza rubia` |

## Cómo ejecutarlo

```bash
ansible-playbook -i inventory-site.yml site.yml
```

El playbook de la rama `dev/david` solo importa este rol.

## Documentación

- [INSTRUCCIONES.md](INSTRUCCIONES.md) — pistas para construir el rol.
- [SOLUCION.md](SOLUCION.md) — versión final lista para revisar.
