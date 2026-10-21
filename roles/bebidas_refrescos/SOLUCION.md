# SOLUCIÓN — Rol bebidas_refrescos

## `roles/bebidas_refrescos/defaults/main.yml`

```yaml
---
seccion_persona: "David"
seccion_nombre: "Bebidas y refrescos"

bebidas_agua: "Agua mineral 1.5L"
bebidas_zumo_naranja: "Zumo de naranja natural"
bebidas_zumo_manzana: "Zumo de manzana"

refrescos_cola: "Refresco de cola"
refrescos_limon: "Refresco de limón"
refrescos_naranja: "Refresco de naranja"

cerveza: "Cerveza rubia"
```

## `roles/bebidas_refrescos/vars/main.yml`

```yaml
---
rol_autor: "David"
rol_seccion: "bebidas y refrescos"
rol_version: "0.1.0"
```

## `roles/bebidas_refrescos/meta/main.yml`

```yaml
---
galaxy_info:
  role_name: bebidas_refrescos
  author: David
  description: Rol educativo que simula la compra de bebidas y refrescos.
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

## `roles/bebidas_refrescos/tasks/main.yml`

```yaml
---
- name: "Mostrar sección que gestiona {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Sección: {{ seccion_nombre }}"

- name: "Listar bebidas sin alcohol"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (bebida): {{ item }}"
  loop:
    - "{{ bebidas_agua }}"
    - "{{ bebidas_zumo_naranja }}"
    - "{{ bebidas_zumo_manzana }}"

- name: "Listar refrescos"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (refresco): {{ item }}"
  loop:
    - "{{ refrescos_cola }}"
    - "{{ refrescos_limon }}"
    - "{{ refrescos_naranja }}"

- name: "Listar otras bebidas"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (otro): {{ item }}"
  loop:
    - "{{ cerveza }}"

- name: "Notificar fin de la compra de {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Compra de {{ seccion_nombre }} completada"
```

## `site.yml` (en raíz, rama dev/david)

```yaml
---
- name: Compra de la familia — David (bebidas y refrescos)
  hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - name: Cargar el rol de bebidas y refrescos
      import_role:
        name: bebidas_refrescos
```

> No existe `roles/bebidas_refrescos/handlers/`.
