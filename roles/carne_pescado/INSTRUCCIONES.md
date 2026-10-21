# INSTRUCCIONES — Rol carne_pescado (Moisés)

Tutorial paso a paso. Si te atascas, [SOLUCION.md](SOLUCION.md) tiene los ficheros completos.

## 1. Objetivo
Imprimir la lista de carnes y pescados que Moisés ha comprado.

## 2. Crear la estructura

```bash
mkdir -p roles/carne_pescado/{defaults,handlers,meta,tasks,vars}
```

## 3. `defaults/main.yml`

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

## 4. `vars/main.yml`

```yaml
---
rol_autor: "Moisés"
rol_seccion: "carne y pescado"
rol_version: "0.1.0"
```

## 5. `meta/main.yml`

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

## 6. `tasks/main.yml`

```yaml
---
- name: "Mostrar sección que gestiona {{ seccion_persona }}"
  ansible.builtin.debug:
    msg: "Sección: {{ seccion_nombre }} (autor: {{ rol_autor }})"

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
  notify: compra_finalizada
```

## 7. `handlers/main.yml`

```yaml
---
- name: compra_finalizada
  ansible.builtin.debug:
    msg: "Handler 'compra_finalizada' ejecutado por {{ seccion_persona }}"
```

## 8. `site.yml` (raíz, rama dev/moises)

```yaml
---
- name: Compra de la familia — Moisés (carne y pescado)
  hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - name: Cargar el rol de carne y pescado
      import_role:
        name: carne_pescado
```

## 9. Probar

```bash
ansible-playbook -i inventory site.yml --syntax-check
ansible-playbook -i inventory site.yml
```

## 10. Commitear

```bash
git add .
git commit -m "feat(role): add carne_pescado role - Moises"
```

## 11. Patrón survey

Igual que el resto: en la rama `survey`, los defaults pasan a
`{{ carne_pollo_survey }}`, `{{ pescado_salmon_survey }}`... y los valores
humanos se aportan con `vars_files` o `-e`.
