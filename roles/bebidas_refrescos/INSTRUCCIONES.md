# INSTRUCCIONES — Rol bebidas_refrescos (David)

Pistas para construir el rol paso a paso. Si te atascas, mira
[SOLUCION.md](SOLUCION.md).

## 1. Objetivo
Imprimir la lista de bebidas y refrescos que David ha comprado, usando
`ansible.builtin.debug`.

## 2. Crea la estructura de carpetas

```bash
mkdir -p roles/bebidas_refrescos/{defaults,meta,tasks,vars}
```

> **No** crees `handlers/`. Este proyecto no usa handlers.

## 3. `defaults/main.yml`

Declara las variables con valores humanos. Convención: `<categoria>_<producto>`.

Pista: 3 bebidas sin alcohol (agua + 2 zumos), 3 refrescos (cola, limón,
naranja) y 1 cerveza. Total: 7 variables de productos más las 2 generales
(`seccion_persona`, `seccion_nombre`).

## 4. `vars/main.yml`

Igual que en los otros roles: autor, sección y versión. **Mayor precedencia**
que `defaults`.

## 5. `meta/main.yml`

Define `galaxy_info` con `author: David`, plataforma `local`, tags
`learning, family, compras`, y `dependencies: []`.

## 6. `tasks/main.yml`

Tareas `debug` con `msg`. Pista:

```yaml
- name: "..."
  ansible.builtin.debug:
    msg: "..."
```

Orden sugerido:
1. Mensaje de sección: `"Sección: {{ seccion_nombre }}"`.
2. `loop:` por las bebidas sin alcohol.
3. `loop:` por los refrescos.
4. `loop:` por la cerveza (un solo elemento).
5. Mensaje final de "compra completada".

## 7. Crear `site.yml` (raíz, rama dev/david) importando solo este rol

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

## 8. Probar

```bash
ansible-playbook -i inventory-site.yml site.yml --syntax-check
ansible-playbook -i inventory-site.yml site.yml
```

## 9. Commitear

```bash
git add .
git commit -m "feat(role): add bebidas_refrescos role - David"
```
