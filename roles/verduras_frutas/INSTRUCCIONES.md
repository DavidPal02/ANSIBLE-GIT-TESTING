# INSTRUCCIONES — Rol verduras_frutas (Ricardo)

Tutorial paso a paso para construir este rol desde cero. Si te atascas, mira
[SOLUCION.md](SOLUCION.md) con los ficheros completos.

## 1. Objetivo
El rol debe imprimir la lista de verduras y frutas que Ricardo ha comprado en el
supermercado, usando variables definidas en `defaults/main.yml` y resolviendo con
`{{ ... }}` en `tasks/main.yml`.

## 2. Crear la estructura de carpetas

Crea esta estructura bajo el directorio `roles/verduras_frutas/`:

```
verduras_frutas/
├── README.md
├── INSTRUCCIONES.md
├── SOLUCION.md
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
└── vars/
    └── main.yml
```

En Linux/macOS:

```bash
mkdir -p roles/verduras_frutas/{defaults,handlers,meta,tasks,vars}
```

## 3. Rellenar `defaults/main.yml` (valores editables por el usuario)

`defaults/main.yml` define variables de **baja precedencia**, fácilmente
sobreescribibles con `-e` o `vars_files`. Son el "menú" del rol.

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

> Cada producto se nombra como `<categoria>_<producto>` para mantener el orden
> y poder localizarlo fácilmente.

## 4. Rellenar `vars/main.yml` (datos internos, no editables)

`vars/main.yml` contiene datos del autor y metadatos. **Mayor precedencia** que
`defaults` — usar solo para datos que el rol asume ciertos.

```yaml
---
rol_autor: "Ricardo"
rol_seccion: "verduras y frutas"
rol_version: "0.1.0"
```

## 5. Rellenar `meta/main.yml` (información para Ansible Galaxy)

`meta/main.yml` describe el rol para `ansible-galaxy`. Importa aunque no se
publique, porque valida dependencias y versión mínima.

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

## 6. Rellenar `tasks/main.yml` (la lógica del rol)

Usa `ansible.builtin.debug` para imprimir los productos. Los `loop` iteran
sobre los valores resueltos de las variables.

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

> `notify: compra_finalizada` dispara el handler solo si la tarea cambia
> (con `debug` siempre será "changed"). Es un ejemplo para mostrar la mecánica.

## 7. Rellenar `handlers/main.yml` (acciones reactivas)

Los handlers se ejecutan al final del play, solo si fueron notificados y solo
si la tarea que los notificó quedó en estado `changed`.

```yaml
---
- name: compra_finalizada
  ansible.builtin.debug:
    msg: "Handler 'compra_finalizada' ejecutado por {{ seccion_persona }}"
```

## 8. Crear `site.yml` en la raíz importando solo este rol

En la rama `dev/ricardo`, `site.yml` debe importar **únicamente** este rol:

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

## 9. Probar

```bash
ansible-playbook -i inventory site.yml --syntax-check
ansible-playbook -i inventory site.yml
```

## 10. Commitear

```bash
git add .
git commit -m "feat(role): add verduras_frutas role - Ricardo"
```

## 11. Convertir los defaults en parametrizables (patrón survey)

Una vez completado el rol, experimenta la mecánica de la rama `survey`:

1. Crea un branch `survey` desde `main`:
   ```bash
   git checkout main
   git checkout -b survey
   ```
2. En `roles/verduras_frutas/defaults/main.yml` renombra las variables a
   `*_survey` y ponles como valor `"{{ verdura_X_survey }}"` (es decir, el
   valor default se convierte en una referencia Jinja2 al nombre `_survey`).
3. En `vars/survey_values.yml` (en la raíz del proyecto) proporciona los
   valores humanos.
4. En `site_survey.yml` importa los roles y añade `vars_files:`.

El motivo de que funcione es el **orden de precedencia** de Ansible:

```
play vars → play vars_files → role vars → role defaults
```

Si en `vars_files` defines `verduras_tomate_survey: "Tomates de Perala"`, la
referencia `{{ verduras_tomate_survey }}` se resuelve allí en lugar de quedar
indefinida.

Mira [SOLUCION.md](SOLUCION.md) para ver la variante survey del `defaults/main.yml`.
