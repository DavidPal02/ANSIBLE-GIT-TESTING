# SOLUCIÓN — Rol carne_pescado

## `roles/carne_pescado/defaults/main.yml`

```yaml
---
seccion_persona: "Moisés"
seccion_nombre: "Carne y pescado"

carne_pollo: "Contramuslos de pollo"
carne_pavo: "Pechugas de pavo al ajillo"
carne_ternera: "Filetes de ternera"

pescado_salmon: "Salmón fresco"
pescado_merluza: "Merluza en rodajas"
```

## `roles/carne_pescado/vars/main.yml`

```yaml
---
rol_autor: "Moisés"
rol_seccion: "carne y pescado"
rol_version: "0.1.0"
```

## `roles/carne_pescado/meta/main.yml`

```yaml
---
galaxy_info:
  role_name: carne_pescado
  author: Moisés
  description: Rol educativo que simula la compra de carne y pescado.
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

## `roles/carne_pescado/tasks/main.yml`

```yaml
---
- name: "Preparar carpeta para la compra del rol carne_pescado"
  ansible.builtin.shell: |
    DIR=/tmp/compras/moises/carne_pescado
    mkdir -p "$DIR"
    echo "Sección: Carne y pescado (Moisés)"
  changed_when: false

- name: "Apuntar carnes compradas (un archivo por producto)"
  ansible.builtin.shell: |
    DIR=/tmp/compras/moises/carne_pescado
    {
      echo "Contramuslos de pollo"       > "$DIR/pollo.txt"
      echo "Pechugas de pavo al ajillo"  > "$DIR/pavo.txt"
      echo "Filetes de ternera"          > "$DIR/ternera.txt"
    }
  args:
    executable: /bin/bash
  changed_when: false

- name: "Apuntar pescados comprados (un archivo por producto)"
  ansible.builtin.shell: |
    DIR=/tmp/compras/moises/carne_pescado
    {
      echo "Salmón fresco"      > "$DIR/salmon.txt"
      echo "Merluza en rodajas" > "$DIR/merluza.txt"
    }
  args:
    executable: /bin/bash
  changed_when: false

- name: "Mostrar resumen final de la compra"
  ansible.builtin.shell: |
    echo "--- Compra de carne y pescado completada ---"
    ls /tmp/compras/moises/carne_pescado
  changed_when: false
```

> No existe `roles/carne_pescado/handlers/`.
