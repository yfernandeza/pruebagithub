## Template: Descripción de PR para Colaboradores

Usa este template al crear pull requests:

```markdown
## 📝 Descripción
Describe brevemente qué cambios haces y por qué.

## 🎯 Tipo de Cambio
Marca el tipo de cambio:
- [ ] 📚 Documentación
- [ ] ✨ Nueva funcionalidad
- [ ] 🐛 Bug fix
- [ ] 🔄 Refactorización
- [ ] ⚡ Breaking change

## 📋 Cambios Clave
- Cambio 1
- Cambio 2
- Cambio 3

## ✅ Checklist de Contribuidor
- [ ] Leí el CONTRIBUTING.md
- [ ] Mi código sigue el estilo del proyecto
- [ ] Agregué documentación de cambios
- [ ] Mis commits tienen mensajes descriptivos
- [ ] No hay conflictos con la rama base
- [ ] He probado los cambios localmente

## 🔗 Issues Relacionados
- Closes #123
- Related to #456

## 📸 Screenshots (si aplica)
Adjunta imágenes si es relevante.

## 📝 Notas Adicionales
Cualquier información extra que sea útil para el revisor.
```

## Template: Descripción de Issue

Usa este template al reportar issues:

```markdown
## 📝 Descripción del Problema
Describe claramente el problema.

## 🔄 Pasos para Reproducir
1. Paso 1
2. Paso 2
3. Paso 3

## ❌ Comportamiento Actual
Qué ocurre actualmente (incorrecto)

## ✅ Comportamiento Esperado
Qué debería ocurrir

## 📋 Información del Sistema
- OS: Windows / macOS / Linux
- Git version: `git --version`
- Browser (si aplica): Chrome / Firefox

## 📸 Screenshots o Logs
Adjunta evidencia del problema.

## Notas Adicionales
Información extra relevante.
```

## Comandos Rápidos para Colaboradores

```bash
# Ver status en cualquier momento
git status

# Ver cambios locales
git diff

# Ver cambios preparados
git diff --cached

# Ver commits de tu rama
git log feature/tu-rama --oneline

# Comparar tu rama con main
git log main..feature/tu-rama --oneline

# Sincronizar con upstream
git fetch upstream
git rebase upstream/main

# Limpiar ramas locales borradas en remoto
git remote prune origin
git fetch --prune

# Stash si necesitas cambiar de rama
git stash

# Ver stash
git stash list

# Aplicar stash
git stash pop

# Configurar editor de git
git config --global core.editor "tu-editor"
```

## Buenas Prácticas de Commits para Colaboradores

```bash
# ✅ BUENO: Pequeños, enfocados
git commit -m "docs: agregar instrucciones de instalación"
git commit -m "fix: corregir enlace en documentación"

# ❌ MALO: Demasiado grande
git commit -m "cambios varios"

# ✅ BUENO: Mensaje descriptivo
git commit -m "feat: agregar validación de email

- Validación de formato
- Mensajes de error personalizados
- Tests unitarios"

# ❌ MALO: Mensaje vago
git commit -m "update"
```

## Proceso de Review en GitHub

1. **Tu creaste PR** ✅
2. **Mantenedor revisa** 👀
   - Puede dejar comentarios
   - Puede solicitar cambios
   - Puede aprobar
3. **Respondes feedback** 📝
   - Haces cambios locales
   - Haces nuevo commit
   - Push automáticamente aparece en PR
4. **Reiterar si es necesario** 🔄
5. **Merge cuando esté aprobado** ✨

## Cómo Responder Feedback

```bash
# Mantenedor solicita cambios

# 1. Ver comentarios en GitHub
# 2. Hacer cambios locales
# 3. Ver status
git status

# 4. Preparar cambios
git add archivo-corregido.md

# 5. Commit (NO hagas --amend)
# Haz nuevo commit con cambios
git commit -m "review: aplicar feedback - mejorar ejemplos"

# 6. Push
git push origin feature/tu-rama

# El PR se actualiza automáticamente con el nuevo commit
```

## Escalada de Problemas

Si tienes dudas o problemas:

1. **Revisa las issues existentes** - Quizás ya se habló del tema
2. **Lee el CONTRIBUTING.md** - Tiene instrucciones específicas
3. **Comenta en el PR** - Los mantenedores te ayudarán
4. **Crea una Discussion** - Para preguntas generales
5. **IRC/Discord/Slack** - Si el proyecto tiene comunidad

---

**¡Recuerda: Todo el mundo fue principiante alguna vez!** 🌟
