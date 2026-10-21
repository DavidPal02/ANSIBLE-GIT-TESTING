# SOLUCIÓN — Rol lacteos_galletas

## `roles/lacteos_galletas/defaults/main.yml`

```yaml
---
seccion_persona: "Ángela"
seccion_nombre: "Lácteos y galletas"

lacteos_leche: "Leche entera"
lacteos_yogur: "Yogur natural"
lacteos_queso: "Queso manchego"

galletas_chocolate: "Galletas con pepitas de chocolate"
galletas_maria: "Galletas María"
```

## `roles/lacteos_galletas/vars/main.yml`

```yaml
---
rol_autor: "Ángela"
rol_seccion: "lácteos y galletas"
rol_version: "0.1.0"
```

## `roles/lacteos_galletas/meta/main.yml`

```yaml
---
galaxy_info:
  role_name: lacteos_galletas
  author: Ángela
  description: Rol educativo que simula la compra de lácteos y galletas.
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

## `roles/lacteos_galletas/tasks/main.yml`

```yaml
---
- name: "Mostrar sección que gestiona {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Sección: {{ seccion_nombre }}"

- name: "Listar lácteos comprados"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (lácteo): {{ item }}"
  loop:
    - "{{ lacteos_leche }}"
    - "{{ lacteos_yogur }}"
    - "{{ lacteos_queso }}"

- name: "Listar galletas compradas"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (galleta): {{ item }}"
  loop:
    - "{{ galletas_chocolate }}"
    - "{{ galletas_maria }}"

- name: "Notificar fin de la compra de {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Compra de {{ seccion_nombre }} completada"
```

> No existe `roles/lacteos_galletas/handlers/`.
