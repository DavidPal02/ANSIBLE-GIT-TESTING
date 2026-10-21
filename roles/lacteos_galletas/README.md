# Rol: lacteos_galletas

Rol educativo que simula la sección de **lácteos y galletas** de la compra
familiar. Responsable: **Ángela**.

## Variables por defecto

| Variable | Valor por defecto |
|---|---|
| `seccion_persona` | `Ángela` |
| `seccion_nombre` | `Lácteos y galletas` |
| `lacteos_leche` | `Leche entera` |
| `lacteos_yogur` | `Yogur natural` |
| `lacteos_queso` | `Queso manchego` |
| `galletas_chocolate` | `Galletas con pepitas de chocolate` |
| `galletas_maria` | `Galletas María` |

## Cómo ejecutarlo aislado

```bash
ansible-playbook -i inventory site.yml
```

El playbook de la rama `dev/angela` solo importa este rol.

## Documentación

- [INSTRUCCIONES.md](INSTRUCCIONES.md) — tutorial paso a paso para crear el rol.
- [SOLUCION.md](SOLUCION.md) — ficheros completos listos para copiar y pegar.

## Variables survey

| Variable en rama survey | Equivalente literal |
|---|---|
| `lacteos_leche_survey` | `lacteos_leche` |
| `lacteos_yogur_survey` | `lacteos_yogur` |
| `lacteos_queso_survey` | `lacteos_queso` |
| `galletas_chocolate_survey` | `galletas_chocolate` |
| `galletas_maria_survey` | `galletas_maria` |
