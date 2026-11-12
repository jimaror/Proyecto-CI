# COMANDOS PARA DIGITAR - Tarea C3 (PowerShell)

> Copiá cada línea en la terminal de VS Code, presioná **Enter**, y tomá la
> captura con **Win + Shift + S** (recorta justo la terminal).
>
> Todos son de **solo lectura**: no modifican nada, podés repetirlos.
>
> **Importante:** después de cada bloque, la terminal muestra la salida.
> Si no ves nada, es que la terminal no tiene foco: hacé **clic** dentro
> de la terminal antes de escribir.

---

## 0. Ubicarte en la carpeta del proyecto

```
cd "C:\Users\JMarkz\Desktop\Clase 3"
```

```
git status
```

```
git rev-list --count HEAD
```

```
git config --global alias.g "log --oneline --graph --all --decorate"
```

```
git g
```

> Debe decir: `nothing to commit, working tree clean` y `21`

---

## 1. CAPTURA - El grafo del repositorio

```
git log --oneline --graph --all --decorate
```

> Sale el árbol con `*`, `|\` y `|/`. Esta es la captura más importante.

---

## 2. CAPTURA - Los dos padres del merge

```
git show --oneline -s 98ece63^1
```

```
git show --oneline -s 98ece63^2
```

> Primero: `5b96c55 Nuevo pie de página`
> Segundo: `12b85ce Nuevo pie de página`

---

## 3. CAPTURA - Inspección del historial

```
git log --stat -1
```

```
git log --grep="sección" --oneline
```

```
git log -S "conflicto" --oneline
```

```
git log --oneline --author="Jimmy"
```

```
git shortlog -sn HEAD
```

---

## 4. CAPTURA - git blame (quién escribió cada línea)

```
findstr /n "header" index.html
```

```
git blame -L 25,30 index.html
```

> Sale: hash | autor | fecha | número de línea | contenido

---

## 5. CAPTURA - Comparación de versiones

```
git show HEAD~3 --stat
```

```
git diff HEAD~5 HEAD --stat
```

```
git diff HEAD~5 HEAD -- index.html
```

```
git diff origin/main main --stat
```

```
git show HEAD~19:index.html
```

---

## 6. CAPTURA - El revert

```
git log --oneline -3
```

```
git log --oneline --decorate -4
```

> Debe verse: `Revert "Prueba fondo rojo"`

---

## 7. CAPTURA - Detached HEAD

```
git log --oneline HEAD~9 HEAD~8
```

---

## 8. CAPTURA - El rescate con reflog

```
git reflog -10
```

> Debe verse la línea: `commit: Nota tres`

---

## 9. CAPTURA - La etiqueta v1.0 y las ramas

```
git tag
```

```
git log --oneline --decorate -4
```

```
git branch -v
```

```
git branch -a
```

```
git branch --show-current
```

> `git branch -v` muestra cada rama con su último commit (más útil para la
> captura que `git branch` a secas). El `*` marca la rama activa.
> `git branch --show-current` imprime solo `main`.

---

## 10. CAPTURA - Las 5 respuestas verificadas

```
(git log --grep="sección" --oneline | Measure-Object -Line).Lines
```

```
git log -S "conflicto" --oneline --reverse
```

```
git blame -L 28,28 index.html
```

```
(git show HEAD~19:index.html | Select-String "<section>" | Measure-Object -Line).Lines
```

```
git log --oneline origin/main..main
```

> **Importante:** el `.Lines` va **al final**, dentro del paréntesis.
> Sin `.Lines` PowerShell muestra una tabla y no el número.

---

# NOTAS

## TRUCO para que se vea toda la salida en la captura

La terminal de VS Code es chica y a veces se te scrollea, entonces no se ve
el comando completo. **Hacé esto antes de cada bloque:**

1. Presioná **`Ctrl + L`** → limpia la terminal (o escribí `cls` + Enter)
2. Después corré tus comandos
3. Tomá la captura

Además, para ver **más líneas**, maximizá el panel de la terminal:
- Click en el ícono de **maximizar** (el ⛶ junto a la papelera, arriba a la derecha de "Terminal")
- o arrastrá el borde hacia arriba

> Con `Ctrl + L` + terminal maximizada vas a ver cada comando completo con
> su salida. Ideal para las capturas.

## Por qué `HEAD~19` y no `HEAD~20`?

La guía dice usar `HEAD~20`, pero tu repo **no tiene 21 commits en la cadena
de primer padre** (tiene 20). `HEAD~20` da error:

```
fatal: ambiguous argument 'HEAD~20'
```

`HEAD~19` sí funciona y es **el primer commit** del repositorio.

> Nota: `git rev-list --count HEAD` dice 21 porque cuenta también los
> commits de las ramas fusionadas, pero `HEAD~N` sigue solo el primer padre.

## Si la terminal se queda pegada

Ves `:` o `(END)` abajo de la pantalla → presioná **`q`**.

## Si un comando no devuelve nada

Hacé **clic dentro de la terminal** primero (a veces el foco está en el
editor). Después fijá el **acento** en `sección`: si tu teclado no lo
escribe, usá este comando equivalente:

```
git log --grep="secci" --oneline
```

---

# RESPUESTAS (para el PDF)

| # | Pregunta | Respuesta |
|---|----------|-----------|
| 1 | Commits que mencionan "sección" | **1** → `a5992bf Agrega sección de ramas` |
| 2 | Commit que **agregó** "conflicto" | **`203d77f`** "Bitácora completa sin conflictos" (el más antiguo) |
| 3 | Autor del subtítulo del `<header>` | **Jimmy Javier Marquez Orozco**, commit **`4587bbe`** (línea 28) |
| 4 | Secciones en la versión más vieja | **1** (en `HEAD~19`, el primer commit) |
| 5 | Commits locales sin subir | **0** (todo está subido) |
