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

## 9. Abrir Pull Request hacia `main`

Tienes dos caminos según dónde esté el remoto canónico.

### 9.1 Si usas GitHub

```bash
# Asegúrate de tener tu rama al día con origin (o github).
git push origin dev/ricardo        # o: git push github dev/ricardo

# Crear la PR desde la terminal con la CLI de GitHub (gh).
# Requiere: gh auth login hecho una vez.
gh pr create \
  --base main \
  --head dev/ricardo \
  --title "feat(role): add verduras_frutas role - Ricardo" \
  --body  "Añade el rol verduras_frutas (Ricardo) y su site.yml mínimo."
```

Si prefieres la web:

```bash
# Solo empuja, luego abre el enlace que devuelve.
git push origin dev/ricardo
# GitHub te imprimirá: "Create a new pull request for 'dev/ricardo'"
# → https://github.com/<tu-org>/ANSIBLE-GIT-TESTING/pulls/new/dev/ricardo
```

### 9.2 Si usas Gitea

```bash
git push origin dev/ricardo
# En la UI de Gitea: Repository → Pull Requests → New Pull Request
# base: main   compare: dev/ricardo
```

Equivalente desde la API REST de Gitea (asume variable
`$GITEA_API` apuntando al repo, p. ej.
`http://gitea:3000/api/v1/repos/PalDevOps-AWX/ANSIBLE-GIT-TESTING`):

```bash
TOKEN=xxxxxxxxxxxx
curl -s -u "$GITEA_USER:$TOKEN" -X POST \
  -H "Content-Type: application/json" \
  -d '{
        "head": "dev/ricardo",
        "base": "main",
        "title": "feat(role): add verduras_frutas role - Ricardo"
      }' \
  "$GITEA_API/pulls"
```

### 9.3 Buenas prácticas

- **Rebase primero** si `main` ha avanzado:
  ```bash
  git fetch origin main
  git rebase origin/main
  git push origin dev/ricardo --force-with-lease
  ```
- **No mezcles roles**: tu PR solo trae tu propio rol más la actualización del
  `site.yml` que sea necesaria. Si hay conflicto en `site.yml`, resuélvelo a
  favor de la versión de `main` (que importa los 4 roles).
- **Una vez mergeada la PR**, `main` ejecutará los 4 roles y mostrará la compra
  completa:
  ```bash
  git checkout main
  git pull
  ansible-playbook -i inventory-site.yml site.yml
  ```
