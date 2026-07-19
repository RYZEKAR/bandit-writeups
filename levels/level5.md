# Nivel 5 → Nivel 6

## Objetivo

Conectarse al nivel 5 de Bandit y encontrar un archivo que cumple tres condiciones específicas: tamaño exacto de 1033 bytes, no ejecutable y ser un archivo regular.

---

## Conceptos

- **Comando `find`:** Busca archivos y directorios según múltiples criterios (tipo, tamaño, permisos, nombre, etc.).
- **`-type f`:** Filtra solo archivos regulares (excluye directorios, enlaces, etc.).
- **`-size 1033c`:** Busca archivos con tamaño exacto de 1033 bytes (`c` = bytes).
- **`! -executable`:** Filtra archivos que NO tengan permiso de ejecución.
- **Combinación de criterios:** `find` permite encadenar condiciones para búsquedas precisas.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **find** — Buscar archivos con filtros
- **cat** — Leer archivos
- **cd** — Cambiar de directorio

---

## Comandos utilizados

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 5 (click para revelar)</summary>

`6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`
</details>

### Paso 2: Explorar

```bash
bandit5@bandit:~$ ls
```

**Resultado:** `inhere`

```bash
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
```

**Resultado:**
```
maybehere00  maybehere01  maybehere02  ...  maybehere19
```

20 subdirectorios. Revisar manualmente cada uno sería tedioso.

### Paso 3: Buscar con `find`

El nivel pedía un archivo que fuera:
- Archivo regular (`-type f`)
- De exactamente 1033 bytes (`-size 1033c`)
- Sin permiso de ejecución (`! -executable`)

```bash
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
```

**Resultado:**
```
./maybehere07/.file2
```

Un solo resultado: el archivo `.file2` dentro de `maybehere07`.

### Paso 4: Leer el archivo

```bash
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
```

<details>
<summary>🔑 Contraseña obtenida para bandit6 (click para revelar)</summary>

`pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`
</details>

### Paso 5: Cerrar sesión

```bash
bandit5@bandit:~/inhere$ exit
```

---

## Resultado

Nivel 5 completado. Se usó `find` con tres filtros combinados para localizar exactamente el archivo correcto entre cientos de archivos en 20 directorios.

---

## Lo que aprendí

- `find` es una herramienta poderosa para buscar archivos con criterios específicos.
- Los filtros se pueden combinar: tipo (`-type f`), tamaño (`-size 1033c`), permisos (`! -executable`), y muchos más.
- `-size` acepta sufijos: `c` = bytes, `k` = kilobytes, `M` = megabytes, `G` = gigabytes.
- El operador `!` niega una condición (también se puede usar `-not`).
- Frente a muchos archivos, buscar con `find` es mucho más eficiente que revisar manualmente.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man find`
- `man ls`
- `man cat`

---

## Notas

- `find` también soporta operadores lógicos: `-and` (por defecto al encadenar), `-or` y `-not` (`!`).
- Se puede ejecutar comandos en los resultados con `-exec`.
- Ejemplo útil: `find . -type f -name "*.txt" -exec cat {} \;`
