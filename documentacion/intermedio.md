# 📖 Git Intermedio - Fase 3-5

Aprende técnicas avanzadas de trabajo colaborativo con ramas, PRs e issues.

## Fase 3: Trabajo con Ramas

### 1. Crear y Cambiar Ramas

```bash
# Crear rama
git branch nombre-rama

# Crear y cambiar a rama (forma antigua)
git checkout -b feature/nueva-funcion

# Crear y cambiar a rama (forma moderna)
git switch -c feature/nueva-funcion

# Cambiar de rama
git switch nombre-rama
git checkout nombre-rama

# Ver ramas locales
git branch

# Ver todas las ramas (incluyendo remotas)
git branch -a
# CAMBIO
# Ver ramas con último commit
git branch -v
```

### 2. Eliminar Ramas

```bash
# Eliminar rama local
git branch -d nombre-rama

# Forzar eliminación
git branch -D nombre-rama

# Eliminar rama remota
git push origin --delete nombre-rama
```

### 3. Renombrar Ramas

```bash
# Renombrar rama actual
git branch -m nuevo-nombre

# Renombrar rama específica
git branch -m nombre-viejo nombre-nuevo

# Renombrar en remoto
git push origin --delete nombre-viejo
git push origin -u nombre-nuevo
```

## Fase 4: Merge vs Rebase

### Merge (Fusión Clásica)

```bash
# Estar en rama main
git checkout main

# Fusionar rama feature
git merge feature/nueva-funcion

# Resultado: commit de merge que une ambas ramas
# Historial: no se altera el historial de feature
```

**Ventajas:**
- Preserva historial completo
- Seguro para cambios ya publicados
- Claro qué se fusionó

**Desventajas:**
- Commits de merge pueden saturar el historial
- Historial menos limpio

### Rebase (Rebase Lineal)

```bash
# Estar en rama feature
git checkout feature/nueva-funcion

# Rebase sobre main
git rebase main

# Esto: Toma commits de feature y los aplica sobre main
# Resultado: historial lineal limpio
```

**Ventajas:**
- Historial lineal y limpio
- Fácil de seguir cambios

**Desventajas:**
- Reescribe historial (NO usar en ramas públicas)
- Puede ser confuso para principiantes

### Resolver Conflictos en Merge/Rebase

```bash
# 1. Iniciar merge/rebase
git merge feature/rama
# o
git rebase main

# 2. Git detectará conflictos
# Archivo mostrará:
# <<<<<<< HEAD
# tu código
# =======
# código de la otra rama
# >>>>>>> feature/rama

# 3. Editar manualmente y resolver

# 4. Preparar cambios
git add archivo-resuelto.py

# 5. Completar operación
git merge --continue  # o
git rebase --continue

# Para cancelar en cualquier momento
git merge --abort
git rebase --abort
```

## Fase 5: Pull Requests (PRs)

### Flujo de PR Completo

```bash
# 1. Crear rama local
git checkout -b feature/mi-feature
git switch -c feature/mi-feature

# 2. Hacer cambios y commits
echo "nuevo código" > archivo.py
git add archivo.py
git commit -m "feat: agregar nueva funcionalidad"

# 3. Push a remoto
git push -u origin feature/mi-feature

# 4. En GitHub:
# - Click en "Compare & pull request"
# - O ir a Pull requests > New pull request
# - Seleccionar rama base (main) y rama comparar (feature/mi-feature)
# - Agregar título y descripción
# - Click "Create pull request"

# 5. Si hay cambios solicitados:
git add cambios.py
git commit -m "fix: aplicar cambios solicitados en review"
git push origin feature/mi-feature

# 6. Después que se aprueba:
# En GitHub, click "Merge pull request"

# 7. Actualizar rama main local
git checkout main
git pull origin main

# 8. Borrar rama local
git branch -d feature/mi-feature
```

### Plantilla de PR Descripción

```markdown
## Descripción
Breve descripción de los cambios

## Tipo de cambio
- [ ] Bug fix
- [ ] Nueva funcionalidad
- [ ] Breaking change
- [ ] Cambio de documentación

## ¿Cómo fue probado?
Describe los tests realizados

## Checklist
- [ ] Mi código sigue el estilo del proyecto
- [ ] He actualizado la documentación
- [ ] Mis cambios no generan warnings
- [ ] He probado localmente

## Issues relacionados
Fixes #123
Related to #456
```

### Revisión de PR

```bash
# Revisar cambios antes de mergear
git show origin/feature/rama

# O traer la rama localmente para probar
git checkout -b revisar-pr origin/feature/rama
git checkout main

# Después del review
git merge revisar-pr

# Borrar rama de revisión
git branch -d revisar-pr
```

## Issues (Tickets de Trabajo)

### Crear Issues

En GitHub:
1. Click en "Issues"
2. Click "New issue"
3. Título y descripción
4. Agregar etiquetas
5. Asignar a alguien
6. Click "Submit new issue"

### Vincular Commits a Issues

```bash
# En el mensaje de commit
git commit -m "feat: implementar login

Fixes #42
"

# O en PR description
# Palabras clave: fixes, resolves, closes

# En GitHub, aparecerá automáticamente vinculado
```

### Etiquetas Útiles de Issues

- `bug` - Error reportado
- `feature` - Nueva funcionalidad
- `enhancement` - Mejora existente
- `documentation` - Cambios de docs
- `good first issue` - Para principiantes
- `help wanted` - Se necesita ayuda
- `in progress` - Alguien está trabajando
- `blocked` - Bloqueado por algo

## Flujo de Trabajo Colaborativo Completo

```bash
# 1. Clonar repositorio
git clone https://github.com/usuario/proyecto.git
cd proyecto

# 2. Crear rama desde main actualizado
git checkout main
git pull origin main
git checkout -b feature/tarea-123

# 3. Trabajar
echo "cambios" > archivo.py
git add archivo.py
git commit -m "feat: implementar tarea #123"

# 4. Push
git push -u origin feature/tarea-123

# 5. En GitHub: Create PR, escribir descripción

# 6. Responder a comentarios del review
git add cambios.py
git commit -m "review: ajustar según feedback"
git push origin feature/tarea-123

# 7. Después del merge en GitHub
git checkout main
git pull origin main

# 8. Limpiar
git branch -d feature/tarea-123
git push origin --delete feature/tarea-123
```

## Buenas Prácticas

### Nombres de Ramas
```
feature/nombre-feature      # Nueva funcionalidad
bugfix/nombre-bug           # Corrección de bug
hotfix/nombre-urgente       # Fix urgente en producción
docs/nombre-documentacion   # Cambios de docs
refactor/nombre-mejora      # Refactorización
test/nombre-test            # Tests nuevos
```

### Commits Atómicos
- Un commit = un cambio lógico
- No mezcles múltiples cambios en un commit
- Fácil de revertir si algo falla

### Mensajes de Commit Claros
```
feat: agregar validación de email

Implementó validación de formato de email
con regex en cliente y servidor.

- Validación regex cliente-side
- API validation en backend
- Tests agregados

Fixes #42
```

### Antes de Mergear
- [ ] Todo código está revisado
- [ ] Tests pasan
- [ ] No hay conflictos
- [ ] Documentación actualizada
- [ ] PR description clara

## 🎯 Próximos Pasos

Cuando domine ramas y PRs, pasa a [Git Avanzado](avanzado.md) para aprender sobre rebase interactivo, cherry-pick y más.
