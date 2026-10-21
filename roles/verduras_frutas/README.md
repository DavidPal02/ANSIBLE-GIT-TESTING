# Rol: verduras_frutas

Rol educativo que simula la sección de **verduras y frutas** de la compra familiar.
Responsable: **Ricardo**.

## Variables por defecto

| Variable | Valor por defecto |
|---|---|
| `seccion_persona` | `Ricardo` |
| `seccion_nombre` | `Verduras y frutas` |
| `verduras_tomate` | `Tomates de rama` |
| `verduras_lechuga` | `Lechuga romana` |
| `verduras_pimiento` | `Pimientos rojos` |
| `frutas_manzana` | `Manzanas reineta` |
| `frutas_platano` | `Plátanos de Canarias` |

## Cómo ejecutarlo aislado

```bash
ansible-playbook -i inventory site.yml
```

El playbook de la rama `dev/ricardo` solo importa este rol.

## Documentación

- [INSTRUCCIONES.md](INSTRUCCIONES.md) — tutorial paso a paso para crear el rol.
- [SOLUCION.md](SOLUCION.md) — ficheros completos listos para copiar y pegar.

## Variables survey (parametrización)

Este rol forma parte del ejemplo del branch `survey`, donde los defaults pasan a
referenciar `{{ verduras_tomate_survey }}`, `{{ frutas_manzana_survey }}`, etc.,
permitiendo override por CLI (`-e`) o por `vars_files`.

| Variable en rama survey | Equivalente literal |
|---|---|
| `verduras_tomate_survey` | `verduras_tomate` |
| `verduras_lechuga_survey` | `verduras_lechuga` |
| `verduras_pimiento_survey` | `verduras_pimiento` |
| `frutas_manzana_survey` | `frutas_manzana` |
| `frutas_platano_survey` | `frutas_platano` |
