# 📖 Git Básico - Fase 1-2

Aprende los comandos más esenciales de Git.

## Fase 1: Configuración Inicial

### Instalar Git
```bash
# Windows
choco install git
# macOS
brew install git
# Linux
sudo apt-get install git
```

### Configurar Git
```bash
# Configurar nombre
git config --global user.name "Tu Nombre"

# Configurar email
git config --global user.email "tu@email.com"

# Verificar configuración
git config --list
```

## Fase 2: Operaciones Básicas

### 1. Inicializar un Repositorio
```bash
# Crear carpeta
mkdir mi-proyecto
cd mi-proyecto

# Inicializar git
git init

# Resultado: carpeta .git oculta creada
```

### 2. Verificar el Estado
```bash
git status
```

**Posibles estados:**
- `Untracked files` - Archivos nuevos sin versionar
- `Changes not staged` - Archivos modificados sin preparar
- `Changes to be committed` - Cambios listos para commit

### 3. Preparar Cambios (git add)
```bash
# Preparar archivo específico
git add archivo.txt

# Preparar todos los cambios
git add .

# Preparar interactivamente
git add -i
```

### 4. Confirmar Cambios (git commit)
```bash
# Commit con mensaje
git commit -m "feat: agregar archivo de prueba"

# Commit con descripción larga
git commit -m "feat: agregar validación de usuario" -m "Esta es una descripción más detallada del cambio"

# Amend (modificar commit anterior)
git commit --amend
```

### 5. Ver el Historial (git log)
```bash
# Ver historial completo
git log

# Ver últimos 3 commits
git log -n 3

# Ver en una línea
git log --oneline

# Ver con gráfico de ramas
git log --graph --oneline --all

# Ver cambios específicos
git log -p
```

### 6. Ver Cambios (git diff)
```bash
# Ver cambios no preparados
git diff

# Ver cambios preparados
git diff --cached

# Ver cambios en archivo específico
git diff archivo.txt
```

### 7. Conectar con GitHub

#### Crear repositorio en GitHub
1. Ve a github.com
2. Haz clic en "New repository"
3. Nombre: `mi-proyecto`
4. Copia la URL

#### Agregar remote
```bash
# Agregar remoto
git remote add origin https://github.com/usuario/mi-proyecto.git

# Verificar remoto
git remote -v
```

### 8. Enviar Cambios (git push)
```bash
# Push a rama main/master
git push origin main

# Push con tracking automático
git push -u origin main

# Futuras veces solo necesitas
git push
```

### 9. Traer Cambios (git pull)
```bash
# Traer y fusionar cambios
git pull

# Traer sin fusionar
git fetch

# Fusionar cambios
git merge origin/main
```

## Ejemplo Completo: Primer Commit

```bash
# 1. Crear proyecto
mkdir tutorial-git
cd tutorial-git
git init

# 2. Configurar usuario
git config user.name "Juan Pérez"
git config user.email "juan@example.com"

# 3. Crear archivo
echo "# Mi Proyecto" > README.md

# 4. Preparar cambios
git add README.md

# 5. Ver estado
git status

# 6. Hacer commit
git commit -m "docs: agregar README inicial"

# 7. Ver historial
git log --oneline

# 8. Conectar con GitHub
git remote add origin https://github.com/usuario/tutorial-git.git

# 9. Enviar a GitHub
git push -u origin main
```

## Resumen de Comandos

| Comando | Función |
|---------|---------|
| `git init` | Inicializar repositorio |
| `git status` | Ver estado |
| `git add` | Preparar cambios |
| `git commit` | Confirmar cambios |
| `git log` | Ver historial |
| `git diff` | Ver cambios |
| `git remote` | Gestionar remotos |
| `git push` | Enviar cambios |
| `git pull` | Traer cambios |

## 🎯 Próximos Pasos

Cuando domines estos comandos, pasa a [Git Intermedio](intermedio.md) para aprender sobre ramas y flujos de trabajo más complejos.

