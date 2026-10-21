# Rol: carne_pescado

Rol educativo que simula la sección de **carne y pescado** de la compra familiar.
Responsable: **Moisés**.

## Variables por defecto

| Variable | Valor por defecto |
|---|---|
| `seccion_persona` | `Moisés` |
| `seccion_nombre` | `Carne y pescado` |
| `carne_pollo` | `Contramuslos de pollo` |
| `carne_pavo` | `Pechugas de pavo al ajillo` |
| `carne_ternera` | `Filetes de ternera` |
| `pescado_salmon` | `Salmón fresco` |
| `pescado_merluza` | `Merluza en rodajas` |

## Cómo ejecutarlo aislado

```bash
ansible-playbook -i inventory site.yml
```

El playbook de la rama `dev/moises` solo importa este rol.

## Documentación

- [INSTRUCCIONES.md](INSTRUCCIONES.md) — tutorial paso a paso para crear el rol.
- [SOLUCION.md](SOLUCION.md) — ficheros completos listos para copiar y pegar.

## Variables survey (parametrización)

| Variable en rama survey | Equivalente literal |
|---|---|
| `carne_pollo_survey` | `carne_pollo` |
| `carne_pavo_survey` | `carne_pavo` |
| `carne_ternera_survey` | `carne_ternera` |
| `pescado_salmon_survey` | `pescado_salmon` |
| `pescado_merluza_survey` | `pescado_merluza` |
