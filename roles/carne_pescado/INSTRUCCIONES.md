# INSTRUCCIONES — Rol carne_pescado (Moisés)

> **Pistas estilo bash** para construir el rol. Piénsalo como un script y luego
> adáptalo a la sintaxis de Ansible (que es prácticamente la misma).

## Paso 1 · Carpeta y variables

Pista bash:

```bash
DIR=/tmp/compras/moises/carne_pescado
mkdir -p "$DIR"
```

En Ansible:

- Mete esa `shell:` dentro de una tarea.
- `ansible.builtin.shell` ejecuta cualquier línea como en terminal.

## Paso 2 · Crear un archivo por carne

Pista bash:

```bash
echo "Contramuslos de pollo" > "$DIR/pollo.txt"
echo "Pechugas de pavo al ajillo" > "$DIR/pavo.txt"
echo "Filetes de ternera" > "$DIR/ternera.txt"
```

Truco: mete las 3 líneas en una sola tarea con bloque `|` y
`args: { executable: /bin/bash }`.

## Paso 3 · Crear un archivo por pescado

```bash
echo "Salmón fresco" > "$DIR/salmon.txt"
echo "Merluza en rodajas" > "$DIR/merluza.txt"
```

## Paso 4 · Resumen

```bash
echo "--- Compra completada ---"
ls "$DIR"
```

## Estructura esperada

```
roles/carne_pescado/
├── README.md
├── INSTRUCCIONES.md
├── SOLUCION.md
├── defaults/main.yml
├── meta/main.yml
├── tasks/main.yml
└── vars/main.yml
```

> **No hay carpeta `handlers/`**. Las tareas son `changed_when: false`, no
> necesitan notificaciones.

## Cómo probarlo

```bash
ansible-playbook -i inventory-site.yml site.yml --syntax-check
ansible-playbook -i inventory-site.yml site.yml
ls /tmp/compras/moises/carne_pescado
```
