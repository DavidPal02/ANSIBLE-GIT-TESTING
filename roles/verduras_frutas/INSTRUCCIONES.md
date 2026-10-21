# INSTRUCCIONES — Rol verduras_frutas (Ricardo)

> **Pistas estilo bash** para construir el rol. Piénsalo como un script y luego
> adáptalo a la sintaxis de Ansible (que es prácticamente la misma).

## Paso 1 · Carpeta y variables

Pista bash:

```bash
DIR=/tmp/compras/ricardo/verduras_frutas
mkdir -p "$DIR"
```

En Ansible:

- Mete esa `shell:` dentro de una tarea.
- `ansible.builtin.shell` ejecuta cualquier línea como en terminal.

## Paso 2 · Crear un archivo por verdura

Pista bash:

```bash
echo "Tomates de rama" > "$DIR/tomate.txt"
echo "Lechuga romana" > "$DIR/lechuga.txt"
```

Truco para meter varias líneas en una sola tarea → usa bloque `|` y `args: { executable: /bin/bash }`.

## Paso 3 · Crear un archivo por fruta

Misma idea que el paso 2, pero con los ficheros de frutas.

## Paso 4 · Mostrar un resumen

Pista bash:

```bash
echo "--- Compra completada ---"
ls "$DIR"
```

Igual que antes: una task `ansible.builtin.shell`.

## Estructura esperada

```
roles/verduras_frutas/
├── README.md
├── INSTRUCCIONES.md
├── SOLUCION.md
├── defaults/main.yml   ← nombres y valores humanos (sin tocar)
├── meta/main.yml       ← solo metadata (autor, plataforma local)
├── tasks/main.yml      ← lo que acabas de escribir
└── vars/main.yml       ← autor + rol (metadatos internos)
```

> **Ya no hay carpeta `handlers/`**. Si te la encuentras en ejemplos online,
> ignórala: en este proyecto no la usamos porque las tareas `shell` con
> `changed_when: false` son "idempotentes" sin necesidad de handlers.

## Cómo probarlo

```bash
ansible-playbook -i inventory-site.yml site.yml --syntax-check
ansible-playbook -i inventory-site.yml site.yml
ls /tmp/compras/ricardo/verduras_frutas
```
