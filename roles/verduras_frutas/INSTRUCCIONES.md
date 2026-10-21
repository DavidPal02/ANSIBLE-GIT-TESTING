# INSTRUCCIONES — Rol verduras_frutas (Ricardo)

Pistas para construir el rol paso a paso. Si te atascas, mira
[SOLUCION.md](SOLUCION.md).

## 1. Objetivo
Imprimir la lista de verduras y frutas que Ricardo ha comprado, usando
`ansible.builtin.debug`.

## 2. Crea la estructura de carpetas

```bash
mkdir -p roles/verduras_frutas/{defaults,meta,tasks,vars}
```

> **No** crees `handlers/`. Este proyecto no usa handlers.

## 3. `defaults/main.yml`

Declara las variables con valores humanos. Convención: `<categoria>_<producto>`.

Pista: tomate, lechuga, pimiento (verduras) y manzana, plátano (frutas).

## 4. `vars/main.yml`

Igual que en los otros roles: autor, sección y versión. **Mayor precedencia**
que `defaults`.

## 5. `meta/main.yml`

Define `galaxy_info` con `author: Ricardo`, plataforma `local`, tags
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
2. `loop:` por las verduras.
3. `loop:` por las frutas.
4. Mensaje final de "compra completada".

## 7. Probar

```bash
ansible-playbook -i inventory-site.yml site.yml --syntax-check
ansible-playbook -i inventory-site.yml site.yml
```

## 8. Commitear

```bash
git add .
git commit -m "feat(role): add verduras_frutas role - Ricardo"
```
