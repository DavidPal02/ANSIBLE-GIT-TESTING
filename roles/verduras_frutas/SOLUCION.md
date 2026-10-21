# SOLUCIÓN — Rol verduras_frutas

Ficheros completos del rol. Listos para copiar y pegar.

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
    msg: "Sección: {{ seccion_nombre }} (autor: {{ rol_autor }})"

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
  notify: compra_finalizada
```

## `roles/verduras_frutas/handlers/main.yml`

```yaml
---
- name: compra_finalizada
  ansible.builtin.debug:
    msg: "Handler 'compra_finalizada' ejecutado por {{ seccion_persona }}"
```

## `site.yml` (en raíz, rama dev/ricardo)

```yaml
---
- name: Compra de la familia — Ricardo (verduras y frutas)
  hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - name: Cargar el rol de verduras y frutas
      import_role:
        name: verduras_frutas
```

## Anexo: variante `survey` de `defaults/main.yml`

En la rama `survey` los defaults pasan a ser referencias a variables `*_survey`:

```yaml
---
seccion_persona: "Ricardo"
seccion_nombre: "Verduras y frutas"

verduras_tomate: "{{ verduras_tomate_survey }}"
verduras_lechuga: "{{ verduras_lechuga_survey }}"
verduras_pimiento: "{{ verduras_pimiento_survey }}"

frutas_manzana: "{{ frutas_manzana_survey }}"
frutas_platano: "{{ frutas_platano_survey }}"
```

Y el `tasks/main.yml` se mantiene idéntico (sigue usando `verduras_tomate`,
`frutas_manzana`, etc.). Los valores reales entran vía `vars_files` o `-e`.
