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
- name: "Mostrar sección que gestiona {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Sección: {{ seccion_nombre }}"

- name: "Listar carnes compradas"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (carne): {{ item }}"
  loop:
    - "{{ carne_pollo }}"
    - "{{ carne_pavo }}"
    - "{{ carne_ternera }}"

- name: "Listar pescados comprados"
  ansible.builtin.debug:
    msg: "{{ seccion_persona }} ha comprado (pescado): {{ item }}"
  loop:
    - "{{ pescado_salmon }}"
    - "{{ pescado_merluza }}"

- name: "Notificar fin de la compra de {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Compra de {{ seccion_nombre }} completada"
```

> No existe `roles/carne_pescado/handlers/`.
