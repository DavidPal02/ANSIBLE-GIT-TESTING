# INSTRUCCIONES — Rol lacteos_galletas (Ángela)

Tutorial paso a paso. Si te atascas, [SOLUCION.md](SOLUCION.md) tiene los ficheros completos.

## 1. Objetivo
Imprimir la lista de lácteos y galletas que Ángela ha comprado.

## 2. Crear la estructura

```bash
mkdir -p roles/lacteos_galletas/{defaults,handlers,meta,tasks,vars}
```

## 3. `defaults/main.yml`

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

## 4. `vars/main.yml`

```yaml
---
rol_autor: "Ángela"
rol_seccion: "lácteos y galletas"
rol_version: "0.1.0"
```

## 5. `meta/main.yml`

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

## 6. `tasks/main.yml`

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

## 7. `handlers/main.yml`

```yaml
---
- name: compra_finalizada
  ansible.builtin.debug:
    msg: "Handler 'compra_finalizada' ejecutado por {{ seccion_persona }}"
```

## 8. `site.yml` (raíz, rama dev/angela)

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

## 9. Probar

```bash
ansible-playbook -i inventory site.yml --syntax-check
ansible-playbook -i inventory site.yml
```

## 10. Commitear

```bash
git add .
git commit -m "feat(role): add lacteos_galletas role - Angela"
```

## 11. Patrón survey

Mismo patrón: en la rama `survey`, los defaults pasan a
`{{ lacteos_leche_survey }}`, `{{ galletas_chocolate_survey }}`... y los
valores humanos entran vía `vars_files` o `-e`.
