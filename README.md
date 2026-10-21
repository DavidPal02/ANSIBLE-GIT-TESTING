# La compra de la familia

Proyecto educativo para practicar **Git** (ramas, merges, integración) y
**Ansible** (roles, `import_role`, defaults) usando la metáfora de una familia
haciendo la compra.

## La familia

| Miembro | Rama | Sección de la compra |
|---|---|---|
| Ricardo | `dev/ricardo` | Verduras y frutas |
| Moisés  | `dev/moises`  | Carne y pescado |
| Ángela  | `dev/angela`  | Lácteos y galletas |
| David   | `dev/david`   | Bebidas y refrescos |
| Integración | `main`    | Las cuatro secciones |

## Estructura

```
.
├── README.md
├── CHANGELOG.md
├── .travis.yml
├── site.yml                  # Playbook principal (importa los 3 roles)
├── inventory                 # Inventario simple (localhost)
├── inventory-site.yml        # Inventario dedicado a site.yml
└── roles/
    ├── verduras_frutas/      # Ricardo
    ├── carne_pescado/        # Moisés
    ├── lacteos_galletas/     # Ángela
    └── bebidas_refrescos/    # David
```

Cada rol contiene: `README.md`, `INSTRUCCIONES.md` (pistas), `SOLUCION.md`
(código de referencia), y los directorios estándar `defaults/`, `meta/`,
`tasks/`, `vars/` (sin `handlers/` en este proyecto).

## Cómo ejecutar

```bash
# Validar sintaxis
ansible-playbook -i inventory-site.yml site.yml --syntax-check

# Ejecutar la compra completa (main)
ansible-playbook -i inventory-site.yml site.yml
```

> También está disponible el inventario `inventory` (formato ini simple),
> útil si prefieres `-i inventory`.

## Ramas y qué contiene cada una

| Branch | Qué contiene | Cómo ejecutarlo |
|---|---|---|
| `main` | Proyecto completo (los 4 roles) | `ansible-playbook -i inventory-site.yml site.yml` |
| `dev/ricardo` | Solo verduras/frutas | mismo comando, solo imprime esa sección |
| `dev/moises` | Solo carne/pescado | idem |
| `dev/angela` | Solo lácteos/galletas | idem |
| `dev/david` | Solo bebidas/refrescos | idem |

## Variables por defecto (jugando desde CLI)

Todos los roles exponen variables literales. Para probar override puntual en
ejecución puedes usar `-e`:

```bash
ansible-playbook -i inventory-site.yml site.yml \
  -e "carne_pollo='Pollo al curry' galletas_maria='Digestivas' refrescos_cola='Cola zero'"
```

## CI

El fichero `.travis.yml` instala Ansible y valida el playbook en modo
syntax-check.

## Licencia

MIT
