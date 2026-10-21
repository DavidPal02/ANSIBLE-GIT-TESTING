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
- name: "Mostrar sección que gestiona {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Sección: {{ seccion_nombre }}"

- name: "Listar verduras compradas"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (verdura): {{ item }}"
  loop:
    - "{{ verduras_tomate }}"
    - "{{ verduras_lechuga }}"
    - "{{ verduras_pimiento }}"

- name: "Listar frutas compradas"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (fruta): {{ item }}"
  loop:
    - "{{ frutas_manzana }}"
    - "{{ frutas_platano }}"

- name: "Notificar fin de la compra de {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Compra de {{ seccion_nombre }} completada"
```

> No existe `roles/verduras_frutas/handlers/`.
