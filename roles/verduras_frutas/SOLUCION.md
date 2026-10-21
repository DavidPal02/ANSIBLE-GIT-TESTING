# SOLUCIÓN — Rol verduras_frutas

## `roles/verduras_frutas/defaults/main.yml`

```yaml
---
seccion_persona: "Ricardo"
seccion_nombre: "Verduras y frutas"

verduras_tomate: "Tomates de rama"
verduras_lechuga: "Lechuga romana"
verduras_pimiento: "Pimientos rojos"

frutas_manzana: "Manzanas reineta"
frutas_platano: "Plátanos de Canarias"
```

## `roles/verduras_frutas/vars/main.yml`

```yaml
---
rol_autor: "Ricardo"
rol_seccion: "verduras y frutas"
rol_version: "0.1.0"
```

## `roles/verduras_frutas/meta/main.yml`

```yaml
---
galaxy_info:
  role_name: verduras_frutas
  author: Ricardo
  description: Rol educativo que simula la compra de verduras y frutas.
  license: MIT
  min_ansible_version: "2.14"
  platforms:
    - name: local
      versions:
        - all
  galaxy_tags:
    - learning
    - family
    - compras

dependencies: []
```

## `roles/verduras_frutas/tasks/main.yml`

```yaml
---
- name: "Preparar carpeta para la compra del rol verduras_frutas"
  ansible.builtin.shell: |
    DIR=/tmp/compras/ricardo/verduras_frutas
    mkdir -p "$DIR"
    echo "Sección: Verduras y frutas (Ricardo)"
  changed_when: false

- name: "Apuntar verduras compradas (un archivo por producto)"
  ansible.builtin.shell: |
    DIR=/tmp/compras/ricardo/verduras_frutas
    {
      echo "Tomates de rama"     > "$DIR/tomate.txt"
      echo "Lechuga romana"     > "$DIR/lechuga.txt"
      echo "Pimientos rojos"    > "$DIR/pimiento.txt"
    }
  args:
    executable: /bin/bash
  changed_when: false

- name: "Apuntar frutas compradas (un archivo por producto)"
  ansible.builtin.shell: |
    DIR=/tmp/compras/ricardo/verduras_frutas
    {
      echo "Manzanas reineta"      > "$DIR/manzana.txt"
      echo "Plátanos de Canarias"  > "$DIR/platano.txt"
    }
  args:
    executable: /bin/bash
  changed_when: false

- name: "Mostrar resumen final de la compra"
  ansible.builtin.shell: |
    echo "--- Compra de verduras y frutas completada ---"
    ls /tmp/compras/ricardo/verduras_frutas
  changed_when: false
```

> **No existe** `roles/verduras_frutas/handlers/`. Las tareas son
> `changed_when: false`, no disparan notificaciones.
