# La compra de la familia

Proyecto educativo para practicar **Git** (ramas, merges, integración) y **Ansible** (roles, `import_role`, defaults, vars_files) usando la metáfora de una familia haciendo la compra.

## La familia

| Miembro | Rama | Sección de la compra |
|---|---|---|
| Ricardo | `dev/ricardo` | Verduras y frutas |
| Moisés  | `dev/moises`  | Carne y pescado |
| Ángela  | `dev/angela`  | Lácteos y galletas |
| Integración | `main`    | Las tres secciones |
| Parametrización | `survey` | Las tres, con valores override |

## Estructura

```
.
├── README.md
├── CHANGELOG.md
├── .travis.yml
├── site.yml                  # Playbook principal (importa los 3 roles)
├── site_survey.yml           # Solo en branch survey (vars_files)
├── inventory                 # Inventario simple (localhost)
├── inventory-site.yml        # Inventario dedicado a site.yml
├── vars/
│   └── survey_values.yml     # Solo en branch survey
└── roles/
    ├── verduras_frutas/      # Ricardo
    ├── carne_pescado/        # Moisés
    └── lacteos_galletas/     # Ángela
```

Cada rol contiene: `README.md`, `INSTRUCCIONES.md` (tutorial paso a paso), `SOLUCION.md` (código completo), y los directorios estándar `defaults/`, `handlers/`, `meta/`, `tasks/`, `vars/`.

## Cómo ejecutar

```bash
# Validar sintaxis (inventario dedicado al site.yml)
ansible-playbook -i inventory-site.yml site.yml --syntax-check

# Ejecutar la compra completa (main)
ansible-playbook -i inventory-site.yml site.yml

# Ejecutar la versión parametrizada (rama survey)
ansible-playbook -i inventory-site.yml site_survey.yml

# Override puntual sin tocar archivos (rama survey)
ansible-playbook -i inventory-site.yml site.yml \
  -e "carne_pollo_survey='Contramuslos al curry' pescado_salmon_survey='Salmón salvaje'"
```

> También está disponible `inventory` (formato ini simple con solo `localhost`),
> útil para ejecutar sin pensar en convenciones.

## Ramas y qué contiene cada una

| Branch | Qué contiene | Cómo ejecutarlo |
|---|---|---|
| `main` | Proyecto completo | `ansible-playbook -i inventory site.yml` |
| `dev/ricardo` | Solo verduras/frutas | mismo comando, solo imprime esa sección |
| `dev/moises` | Solo carne/pescado | idem |
| `dev/angela` | Solo lácteos/galletas | idem |
| `survey` | Defaults parametrizables con `_survey` | `site_survey.yml` o `-e` |

## Variables parametrizables (rama `survey`)

| Variable | Default en `defaults/main.yml` |
|---|---|
| `carne_pollo_survey` | `Contramuslos de pollo` |
| `carne_pavo_survey` | `Pechugas de pavo al ajillo` |
| `carne_ternera_survey` | `Filetes de ternera` |
| `pescado_salmon_survey` | `Salmón fresco` |
| `pescado_merluza_survey` | `Merluza en rodajas` |
| `verduras_tomate_survey` | `Tomates de rama` |
| `verduras_lechuga_survey` | `Lechuga romana` |
| `verduras_pimiento_survey` | `Pimientos rojos` |
| `frutas_manzana_survey` | `Manzanas reineta` |
| `frutas_platano_survey` | `Plátanos de Canarias` |
| `lacteos_leche_survey` | `Leche entera` |
| `lacteos_yogur_survey` | `Yogur natural` |
| `lacteos_queso_survey` | `Queso manchego` |
| `galletas_chocolate_survey` | `Galletas con pepitas de chocolate` |
| `galletas_maria_survey` | `Galletas María` |

## CI

El fichero `.travis.yml` instala Ansible y valida el playbook en modo syntax-check.

## Licencia

MIT
