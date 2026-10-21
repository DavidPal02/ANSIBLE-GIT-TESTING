# INSTRUCCIONES — Rol lacteos_galletas (Ángela)

Pistas para construir el rol paso a paso. Si te atascas, mira
[SOLUCION.md](SOLUCION.md).

## 1. Objetivo
Imprimir la lista de lácteos y galletas que Ángela ha comprado, usando
`ansible.builtin.debug` para que la salida sea legible.

## 2. Crea la estructura de carpetas

```bash
mkdir -p roles/lacteos_galletas/{defaults,meta,tasks,vars}
```

> **No** crees `handlers/`. Este proyecto no usa handlers.

## 3. `defaults/main.yml`

Declara las variables con valores humanos. Convención: `<categoria>_<producto>`.

Pista: necesitas variables para leche, yogur, queso y dos tipos de galletas.

## 4. `vars/main.yml`

Igual que en los otros roles: autor, sección y versión. **Mayor precedencia**
que `defaults`.

## 5. `meta/main.yml`

Define `galaxy_info` con `author: Ángela`, plataforma `local`, tags
`learning, family, compras`, y `dependencies: []`.

## 6. `tasks/main.yml`

Una tarea `debug` por mensaje. Pista:

```yaml
- name: "..."
  ansible.builtin.debug:
    msg: "..."
```

Empieza con un mensaje que diga `"Sección: {{ seccion_nombre }}"`, luego un
`loop:` por los lácteos, otro por las galletas, y al final un mensaje de
"compra completada".

## 7. Probar

```bash
ansible-playbook -i inventory-site.yml site.yml --syntax-check
ansible-playbook -i inventory-site.yml site.yml
```

## 8. Commitear

```bash
git add .
git commit -m "feat(role): add lacteos_galletas role - Angela"
```
