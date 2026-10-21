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
    msg: "Sección: {{ seccion_nombre }} (autor: {{ rol_autor }})"

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
  notify: compra_finalizada
```

## `roles/lacteos_galletas/handlers/main.yml`

```yaml
---
- name: compra_finalizada
  ansible.builtin.debug:
    msg: "Handler 'compra_finalizada' ejecutado por {{ seccion_persona }}"
```

## `site.yml` (en raíz, rama dev/angela)

```yaml
---
- name: Compra de la familia — Ángela (lácteos y galletas)
  hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - name: Cargar el rol de lácteos y galletas
      import_role:
        name: lacteos_galletas
```

## Anexo: variante `survey` de `defaults/main.yml`

```yaml
---
seccion_persona: "Ángela"
seccion_nombre: "Lácteos y galletas"

lacteos_leche: "{{ lacteos_leche_survey }}"
lacteos_yogur: "{{ lacteos_yogur_survey }}"
lacteos_queso: "{{ lacteos_queso_survey }}"

galletas_chocolate: "{{ galletas_chocolate_survey }}"
galletas_maria: "{{ galletas_maria_survey }}"
```

Las `tasks` no cambian: siguen llamando a `lacteos_leche`, `galletas_chocolate`, etc.
