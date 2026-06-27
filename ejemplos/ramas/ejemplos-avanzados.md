## Ejemplo Completo: Contribuir a un Proyecto

### Escenario: Agregar Feature a Proyecto Existente

```bash
# 1. Clonar repositorio
git clone https://github.com/usuario/proyecto.git
cd proyecto

# 2. Crear rama
git checkout -b feature/agregar-autenticacion

# 3. Hacer cambios
touch auth.py
echo "def login(user, pass):" > auth.py
git add auth.py
git commit -m "feat: módulo de autenticación base"

# 4. Más cambios
echo "def logout(user):" >> auth.py
git add auth.py
git commit -m "feat: agregar función logout"

# 5. Push
git push -u origin feature/agregar-autenticacion

# 6. En GitHub: Crear PR
# - Describir cambios
# - Agregar referencias a issues

# 7. Si te piden cambios
# - Editar archivos localmente
# - Commit: git commit -m "review: aplicar feedback"
# - Push: git push

# 8. Después de merge en GitHub
git checkout main
git pull origin main
git branch -d feature/agregar-autenticacion
```

## Ejemplo: Resolver Conflicto de Merge

```bash
# Situación: Feature branch tiene conflictos con main

# 1. Estar en feature branch
git checkout feature/mi-feature

# 2. Intentar merge
git merge main
# CONFLICT: Hay conflicto

# 3. Ver archivos con conflicto
git status
# archivo.py:  both modified

# 4. Editar archivo.py manualmente
# Buscar:
# <<<<<<< HEAD
# tu código (feature)
# =======
# código de main
# >>>>>>> main

# 5. Resolver conflicto (elegir uno o combinar)
# Borrar marcadores de conflicto
# Dejar código correcto

# 6. Preparar cambios resueltos
git add archivo.py

# 7. Completar merge
git commit -m "merge: resolver conflicto con main"

# 8. Push
git push origin feature/mi-feature
```

## Ejemplo: Limpiar Historial con Squash

```bash
# Situación: Muchos commits pequeños antes de PR

git log --oneline
# abc1234 fix: typo
# def5678 fix: otro typo
# ghi9012 feat: nueva feature
# jkl3456 feat: más cambios

# Opción 1: Rebase interactivo
git rebase -i HEAD~4
# En editor, cambiar:
# pick ghi9012 feat: nueva feature
# squash jkl3456 feat: más cambios
# squash def5678 fix: otro typo
# squash abc1234 fix: typo

# Guardar y editar mensaje final

# Opción 2: Squash en PR (GitHub hace automáticamente)
# En GitHub, al mergear, elegir "Squash and merge"
```

## Ejemplo: Recuperar Rama Borrada

```bash
# Accidentalmente borré mi rama
git branch -D feature/importante

# 1. Ver reflog para encontrar el commit
git reflog
# abc1234 HEAD@{0}: checkout: moving to main
# def5678 HEAD@{1}: commit: feat: importante

# 2. Crear rama desde ese commit
git checkout -b feature/importante def5678

# ¡Rama recuperada!
```

## Ejemplo: Cherry-Pick para Backport

```bash
# Situación: Fix está en main, necesito en branch de versión anterior

# Ver commit a copiar
git log --oneline main
# abc1234 fix: critical bug

# En rama de versión anterior
git checkout release/v1.0
git cherry-pick abc1234

# Fix está ahora en v1.0 también
```

## Ejemplo: Actualizar Fork

```bash
# Tengo fork de proyecto, quiero actualizar

# 1. Agregar upstream
git remote add upstream https://github.com/original/proyecto.git

# 2. Traer cambios del original
git fetch upstream

# 3. Rebase mi main sobre upstream
git checkout main
git rebase upstream/main

# 4. Push a mi fork
git push origin main --force-with-lease
```

## Tabla de Decisión: ¿Qué Comando Usar?

| Situación | Comando | Razón |
|-----------|---------|-------|
| Cambios locales sin push | `git reset` | Seguro, solo local |
| Cambios ya en remoto | `git revert` | Crea historial limpio |
| Aplicar commit de otra rama | `git cherry-pick` | Específico para ese commit |
| Actualizar feature con main | `git merge main` o `git rebase main` | Merge si ya publicado, rebase si local |
| Eliminar archivo publicado | `git rm` + commit | Rastreable en historial |
| Guardar trabajo temporal | `git stash` | Fácil de recuperar |
| Fusionar commits antes de PR | `git rebase -i` | Limpia historial |
