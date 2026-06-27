# 🚀 Guía de Colaboración en Git y GitHub

Esta guía es diseñada para participantes del taller que quieren contribuir a proyectos open source.

## Paso 1: Fork y Clone

```bash
# 1. En GitHub, click en "Fork"
# Crea copia del repositorio en tu cuenta

# 2. Clonar tu fork
git clone https://github.com/TU_USUARIO/pruebagithub.git
cd pruebagithub

# 3. Agregar upstream (repositorio original)
git remote add upstream https://github.com/yfernandeza/pruebagithub.git

# 4. Verificar remotes
git remote -v
# origin -> tu fork
# upstream -> repositorio original
```

## Paso 2: Crear Rama de Feature

```bash
# 1. Actualizar main local
git checkout main
git pull upstream main

# 2. Crear rama
git checkout -b feature/descripcion-breve

# Ejemplo:
git checkout -b feature/agregar-guia-colaboracion
```

## Paso 3: Hacer Cambios y Commits

```bash
# 1. Editar archivos
# ... cambios ...

# 2. Ver cambios
git status
git diff

# 3. Preparar cambios
git add .

# 4. Commit con mensaje descriptivo
git commit -m "feat: agregar guía de colaboración

- Incluye paso a paso para contribuidores
- Ejemplos prácticos de flujo de trabajo
- Sección de troubleshooting"

# 5. Más cambios si es necesario
git add .
git commit -m "docs: mejorar sección de troubleshooting"
```

## Paso 4: Push a tu Fork

```bash
# Push de rama local a tu fork
git push -u origin feature/descripcion-breve

# Futuras veces solo
git push
```

## Paso 5: Crear Pull Request

### En GitHub:
1. Ve a tu fork
2. Verás banner: "Compare & pull request"
3. Click en "Compare & pull request"
4. Verifica:
   - Base repository: `yfernandeza/pruebagithub`
   - Base branch: `main`
   - Head repository: `tu-usuario/pruebagithub`
   - Compare branch: `feature/descripcion-breve`

### Escribir Descripción:

```markdown
## 📝 Descripción
Agregué una guía de colaboración completa para ayudar a nuevos contribuidores.

## 🎯 Tipo de Cambio
- [x] Documentación
- [ ] Nueva funcionalidad
- [ ] Bug fix
- [ ] Breaking change

## 📋 Cambios Realizados
- Guía paso a paso para fork/clone
- Instrucciones de contribución
- Ejemplos prácticos
- Sección de troubleshooting

## ✅ Checklist
- [x] Lei la documentación existente
- [x] Mis cambios no rompen nada
- [x] Formaté correctamente el markdown
- [x] Agregué ejemplos de código

## 📎 Issues Relacionados
Closes #1 (si aplica)
Related to #2 (si aplica)
```

5. Click en "Create pull request"

## Paso 6: Responder a Reviews

Si el mantenedor solicita cambios:

```bash
# 1. Hacer cambios locales
# ... editar archivos ...

# 2. Ver qué cambió
git diff

# 3. Preparar y commit
git add .
git commit -m "review: aplicar feedback del mantenedor"

# 4. Push (automáticamente aparecerá en el PR)
git push origin feature/descripcion-breve
```

## Paso 7: Después del Merge

```bash
# 1. Actualizar main local
git checkout main
git pull upstream main

# 2. Eliminar rama local
git branch -d feature/descripcion-breve

# 3. Eliminar rama en remoto (opcional)
git push origin --delete feature/descripcion-breve

# 4. Sincronizar tu fork con upstream
git pull upstream main
git push origin main
```

## Troubleshooting Común

### "El PR tiene conflictos"
```bash
# 1. Traer cambios de main
git fetch upstream
git merge upstream/main

# 2. Resolver conflictos manualmente

# 3. Commit y push
git add .
git commit -m "merge: resolver conflictos con main"
git push origin feature/descripcion-breve
```

### "Quiero actualizar mi fork"
```bash
# 1. Traer cambios del original
git fetch upstream

# 2. Rebase mi main
git checkout main
git rebase upstream/main

# 3. Push a mi fork
git push origin main --force-with-lease
```

### "Cometí error en el commit"
```bash
# 1. Ver commits
git log --oneline

# 2. Cambiar último commit
git commit --amend --no-edit

# 3. O cambiar mensaje
git commit --amend -m "nuevo mensaje"

# 4. Push
git push origin feature/descripcion-breve --force-with-lease
```

### "Necesito hacer rebase"
```bash
# 1. Fetch cambios
git fetch upstream

# 2. Rebase sobre main
git rebase upstream/main

# 3. Push con force (en rama feature, seguro)
git push origin feature/descripcion-breve --force-with-lease
```

## Consejos para Contribuidores

### ✅ Haz:
- Commits pequeños y enfocados
- Mensajes claros y descriptivos
- Prueba tus cambios localmente
- Lee el CONTRIBUTING.md del proyecto
- Sé respetuoso en comentarios de PR
- Usa --force-with-lease en lugar de --force

### ❌ No hagas:
- Cambios sin crear issue primero
- Commits gigantes con múltiples cambios
- Mensajes vagos ("fix typo", "updates")
- Usar --force (usa --force-with-lease)
- Reescribir historial de ramas públicas
- Ignorar feedback del revisor

## Flujo Estándar Resumido

```bash
# 1. Actualizar
git checkout main
git pull upstream main

# 2. Crear rama
git checkout -b feature/nombre

# 3. Trabajar
git add .
git commit -m "feat: descripción"

# 4. Push
git push -u origin feature/nombre

# 5. En GitHub: Crear PR

# 6. Responder feedback
git add .
git commit -m "review: feedback"
git push

# 7. Después del merge
git checkout main
git pull upstream main
git branch -d feature/nombre
```

## 🎓 Recursos Adicionales

- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [How to Write Good Commit Messages](https://chris.beams.io/posts/git-commit/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Documentation](https://git-scm.com/doc)

---

**¡Gracias por contribuir al taller!** 🙏
