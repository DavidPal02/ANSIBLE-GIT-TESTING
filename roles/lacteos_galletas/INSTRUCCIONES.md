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

## 9. Abrir Pull Request hacia `main`

Tienes dos caminos según dónde esté el remoto canónico.

### 9.1 Si usas GitHub

```bash
# Asegúrate de tener tu rama al día con origin (o github).
git push origin dev/angela        # o: git push github dev/angela

# Crear la PR desde la terminal con la CLI de GitHub (gh).
# Requiere: gh auth login hecho una vez.
gh pr create \
  --base main \
  --head dev/angela \
  --title "feat(role): add lacteos_galletas role - Angela" \
  --body  "Añade el rol lacteos_galletas (Ángela) y su site.yml mínimo."
```

Si prefieres la web:

```bash
# Solo empuja, luego abre el enlace que devuelve.
git push origin dev/angela
# GitHub te imprimirá: "Create a new pull request for 'dev/angela'"
# → https://github.com/<tu-org>/ANSIBLE-GIT-TESTING/pulls/new/dev/angela
```

### 9.2 Si usas Gitea

```bash
git push origin dev/angela
# En la UI de Gitea: Repository → Pull Requests → New Pull Request
# base: main   compare: dev/angela
```

Equivalente desde la API REST de Gitea (asume variable
`$GITEA_API` apuntando al repo, p. ej.
`http://gitea:3000/api/v1/repos/PalDevOps-AWX/ANSIBLE-GIT-TESTING`):

```bash
TOKEN=xxxxxxxxxxxx
curl -s -u "$GITEA_USER:$TOKEN" -X POST \
  -H "Content-Type: application/json" \
  -d '{
        "head": "dev/angela",
        "base": "main",
        "title": "feat(role): add lacteos_galletas role - Angela"
      }' \
  "$GITEA_API/pulls"
```

### 9.3 Buenas prácticas

- **Rebase primero** si `main` ha avanzado:
  ```bash
  git fetch origin main
  git rebase origin/main
  git push origin dev/angela --force-with-lease
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
