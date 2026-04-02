# Instrucciones: Subir el repositorio a GitHub

Tu repositorio local ya está creado. Ahora sigue estos pasos para subirlo a GitHub:

## PASO 1: Crear repositorio en GitHub

1. Ve a https://github.com/new
2. Nombre del repositorio: `mapa-parque-culturas` (o el que prefieras)
3. Descripción: `Mapa ilustrado del Parque de las Culturas y de la Madre Tierra - Con coordenadas GPS reales, trabajo por capas con Gemini AI`
4. **Selecciona: Público**
5. NO selecciones "Initialize this repository with a README" (tu ya tienes archivos)
6. Clic en **"Create repository"**

GitHub te mostrará una pantalla con instructions. Aparecerá algo como:

```
…or push an existing repository from the command line

git remote add origin https://github.com/TUUSUARIO/mapa-parque-culturas.git
git branch -m main master
git push -u origin master
```

## PASO 2: Ejecutar los comandos que GitHub te da

Copia exactamente los 3 comandos que GitHub muestra (reemplazando TUUSUARIO por tu usuario de GitHub):

### Opción A: Si ya estás autenticado en Git
Abre PowerShell/Terminal en la carpeta MAPA y ejecuta:

```powershell
git remote add origin https://github.com/TUUSUARIO/mapa-parque-culturas.git
git branch -m main master
git push -u origin master
```

### Opción B: Si es tu primer vez o tienes problemas de autenticación

GitHub ya no acepta contraseñas por línea de comandos. Necesitas un **Personal Access Token**:

1. Ve a: https://github.com/settings/tokens
2. Clic en "Generate new token" → "Generate new token (classic)"
3. Dale un nombre: "git-cli" o similar
4. Selecciona estos permisos:
   - ☑ repo (acceso completo a repositorios)
   - ☑ workflow (opcional)
5. Clic en "Generate token"
6. **COPIA EL TOKEN** (no podrás verlo de nuevo)
7. En PowerShell, cuando te pida contraseña, pega el token

## PASO 3: Autenticarse en Git (primera vez)

Si es la primera vez que subes:

```powershell
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@example.com"
```

## PASO 4: Agregar el remote y hacer push

```powershell
cd "c:\Users\pedro\Desktop\MAPA"
git remote add origin https://github.com/TUUSUARIO/mapa-parque-culturas.git
git branch -m main master
git push -u origin master
```

Si te pide autenticación:
- Usuario: tu usuario de GitHub
- Contraseña: **pega aquí tu Personal Access Token** (no tu contraseña de GitHub)

## PASO 5: Verificar

1. Ve a tu repositorio en GitHub: https://github.com/TUUSUARIO/mapa-parque-culturas
2. Deberías ver los archivos:
   - `GUIA_MAPA_CON_GEMINI.md`
   - `original.png`
   - `01_terreno.png`
   - `02_caminos.png`

## Si algo falla

**Error: "remote origin already exists"**
```powershell
git remote remove origin
git remote add origin https://github.com/TUUSUARIO/mapa-parque-culturas.git
```

**Error: "fatal: '[URL]' does not appear to be a 'git' repository"**
Verifica que la URL sea correcta. Debe ser exactamente como te muestra GitHub.

**Error de autenticación**
Asegúrate de:
1. Haber creado el token en GitHub
2. Usar el token (no tu contraseña)
3. Tener permisos "repo" en el token

---

## Próximos pasos (después de subirlo):

1. **Crear archivo `.gitignore`** para ignorar archivos temporales
2. **Agregar README.md** con instrucciones de uso
3. **Crear carpetas organizadas** (capas/, assets/, prompts/)
4. **Hacer commits regularmente** conforme avances en las capas

Para ver el estado de tu repositorio:
```powershell
git status
git log --oneline
```
