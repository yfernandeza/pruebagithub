# 📖 Git Avanzado - Fase 6-10

Técnicas avanzadas para desarrolladores experimentados.

## Fase 6: Tags y Releases

### Crear Tags

```bash
# Tag ligero (solo referencia)
git tag v1.0.0

# Tag anotado (con información)
git tag -a v1.0.0 -m "Versión 1.0.0 - Release inicial"

# Ver tags
git tag

# Ver detalles de tag
git show v1.0.0

# Crear tag en commit específico
git tag v0.9.0 9fceb02
```

### Trabajar con Tags

```bash
# Push tag específico
git push origin v1.0.0

# Push todos los tags
git push origin --tags

# Eliminar tag local
git tag -d v1.0.0

# Eliminar tag remoto
git push origin --delete v1.0.0

# Cambiar a tag específico
git checkout v1.0.0
```

### Versionamiento Semántico

```
v1.2.3
│ │ │
│ │ └─ PATCH (bug fixes)
│ └─── MINOR (nuevas features, backward compatible)
└───── MAJOR (breaking changes)

Ejemplos:
v1.0.0 → v1.0.1  # Bug fix
v1.0.0 → v1.1.0  # Nueva feature
v1.0.0 → v2.0.0  # Breaking change
```

### Crear Release en GitHub

```bash
# Via web: GitHub > Releases > Draft a new release
# O via CLI:

gh release create v1.0.0 --title "Version 1.0.0" \
  --notes "Primera versión estable"

# Con archivos
gh release create v1.0.0 ./app.exe ./app.zip \
  --title "Version 1.0.0"
```

## Fase 7: Revertir y Deshacer Cambios

### Git Reset

```bash
# Ver commits
git log --oneline

# Reset SOFT (mantiene cambios preparados)
git reset --soft HEAD~1
# Cambios vuelven a estar en staging

# Reset MIXED (default - descarta staging)
git reset --mixed HEAD~1
# o simplemente
git reset HEAD~1
# Cambios vuelven a working directory

# Reset HARD (descarta todo)
git reset --hard HEAD~1
# ⚠️ Cuidado: esto elimina cambios

# Reset a commit específico
git reset --hard abc1234
```

### Git Revert

```bash
# Revertir commit específico (crea nuevo commit inverso)
git revert abc1234

# Revertir último commit
git revert HEAD

# Revertir múltiples commits
git revert HEAD~2..HEAD

# Sin hacer commit automáticamente
git revert --no-commit abc1234
```

**Diferencia:**
- `reset` - Elimina commits (solo en ramas locales)
- `revert` - Crea commit inverso (seguro en ramas públicas)

### Git Restore

```bash
# Descartar cambios en working directory
git restore archivo.py

# Restaurar desde staging
git restore --staged archivo.py

# Restaurar archivo a commit específico
git restore --source=HEAD~1 archivo.py

# Restaurar todo a último commit
git restore .
```

### Git Clean

```bash
# Ver qué sería eliminado (dry run)
git clean -n

# Eliminar archivos no rastreados
git clean -f

# Eliminar archivos y carpetas no rastreadas
git clean -fd

# Eliminar también archivos ignorados
git clean -fdx
```

## Fase 8: Stash

### Guardar Cambios Temporales

```bash
# Guardar cambios
git stash

# Guardar con descripción
git stash save "descripción del cambio"

# Guardar incluyendo untracked files
git stash -u

# Listar todos los stashes
git stash list

# Ver contenido de stash
git stash show
git stash show -p stash@{0}
```

### Aplicar Stash

```bash
# Aplicar último stash (mantiene el stash)
git stash apply

# Aplicar stash específico
git stash apply stash@{0}

# Aplicar y eliminar (pop)
git stash pop

# Pop stash específico
git stash pop stash@{1}

# Eliminar stash
git stash drop stash@{0}

# Eliminar todos los stashes
git stash clear
```

### Crear Rama desde Stash

```bash
# Útil si el stash no aplica limpiamente
git stash branch nueva-rama stash@{0}
```

## Fase 9: Historial y Búsqueda

### Git Log Avanzado

```bash
# Mostrar cambios (difícil)
git log -p

# Mostrar stats de cambios
git log --stat

# Una línea por commit
git log --oneline

# Gráfico de ramas
git log --graph --oneline --all

# Por autor
git log --author="Juan"

# En rango de fechas
git log --since="2 weeks ago"
git log --after="2023-01-01" --before="2023-12-31"

# Por mensaje
git log --grep="feat:"

# Commits de un archivo específico
git log archivo.py

# Formato personalizado
git log --format="%h %an %s"
# %h = hash corto
# %an = nombre autor
# %s = subject/mensaje

# Reverse (más viejo primero)
git log --reverse
```

### Git Grep (Búsqueda en Código)

```bash
# Buscar en archivos rastreados
git grep "función"

# Buscar en rama específica
git grep "función" origin/main

# Mostrar número de línea
git grep -n "función"

# Buscar en commit específico
git grep "función" v1.0.0

# Caso insensible
git grep -i "FUNCION"
```

### Git Blame (Rastrear Cambios)

```bash
# Ver quién cambió cada línea
git blame archivo.py

# Con fecha
git blame -l archivo.py

# Ver solo rango de líneas
git blame -L 10,20 archivo.py

# Ignorar espacios en blanco
git blame -w archivo.py
```

### Git Show

```bash
# Ver detalles de commit
git show abc1234

# Ver archivo en commit específico
git show abc1234:archivo.py

# Ver cambios de commit
git show --stat abc1234
```

## Fase 10: Rebase Interactivo y Técnicas Avanzadas

### Rebase Interactivo

```bash
# Rebase últimos 3 commits
git rebase -i HEAD~3

# Opciones en editor:
# pick      - usar commit
# reword    - cambiar mensaje
# squash    - fusionar con anterior
# fixup     - fusionar sin mensaje
# drop      - eliminar commit
# exec      - ejecutar comando

# Ejemplo: fusionar últimos 2 commits
git rebase -i HEAD~2
# Cambiar "pick" del 2do a "squash"
# Guardar y editar mensaje del commit fusionado
```

### Cherry-Pick

```bash
# Aplicar commit específico a rama actual
git cherry-pick abc1234

# Cherry-pick múltiples commits
git cherry-pick abc1234 def5678 ghi9012

# Cherry-pick rango
git cherry-pick abc1234..def5678

# Sin hacer commit automáticamente
git cherry-pick --no-commit abc1234

# Si hay conflictos
git cherry-pick --continue
git cherry-pick --abort
```

### Reflog (Reference Logs)

```bash
# Ver historial de cambios de HEAD
git reflog

# Recuperar commit perdido
git reflog
git checkout abc1234  # Recuperar

# Revertir reset peligroso
git reflog
git reset --hard abc1234
```

### Búsqueda Binaria

```bash
# Encontrar commit que introdujo bug
git bisect start
git bisect bad HEAD
git bisect good v1.0.0

# Git te dará commits para probar
# Si tiene bug: git bisect bad
# Si no tiene: git bisect good

# Cuando termines
git bisect reset
```

## Flujos de Trabajo Avanzados

### Workflow GitHub Flow

```bash
1. Crear rama desde main
2. Hacer commits descriptivos
3. Crear PR
4. Discutir y revisar
5. Merge a main
6. Deploy

Ideal para: Proyectos continuos
```

### Workflow Git Flow

```bash
main (producción)
  ↓
release branches
  ↓
develop
  ↑
feature branches
  ↑
hotfix branches (de main)

Ideal para: Proyectos con versiones
```

## Aliases Útiles

```bash
# Agregar aliases
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'restore --staged'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --graph --oneline --all'

# Luego usar
git co main
git br -a
git visual
```

## Seguridad y Buenas Prácticas

### GPG Signing

```bash
# Firmar commit
git commit -S -m "mensaje"

# Configurar firma por defecto
git config --global user.signingkey <KEY_ID>
git config --global commit.gpgsign true
```

### Proteger Ramas

En GitHub:
1. Settings > Branches > Branch protection rules
2. Crear regla para main:
   - Requerir PR review
   - Requerir status checks
   - Requerir ramas actualizadas

### Secretos en Git

```bash
# Buscar secretos en historial
git log -p | grep -i "password"

# Usar herramientas
# - git-secrets
# - detect-secrets
# - truffleHog
```

## Troubleshooting Común

```bash
# Deshacer push público (peligroso)
git push --force-with-lease origin main

# Recuperar rama borrada
git reflog
git checkout -b rama abc1234

# Cambiar último commit
git commit --amend

# Cambiar autor de commits pasados
git rebase -i HEAD~3
# Cambiar "pick" a "edit"
git commit --amend --author="Nuevo Autor"
git rebase --continue

# Ver cambios no commiteados
git diff
git diff --cached

# Limpiar tracking remoto
git remote prune origin
```

## 🎯 ¡Felicidades!

Has completado el taller avanzado de Git. Ahora puedes:
- ✅ Manejar ramas complejas
- ✅ Hacer rebase interactivo
- ✅ Buscar y rastrear cambios
- ✅ Recuperar cambios perdidos
- ✅ Collaborar efectivamente

¡A seguir aprendiendo! 🚀
