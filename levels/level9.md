# Nivel 9 → Nivel 10

## Objetivo

Conectarse al nivel 9 de Bandit y extraer cadenas de texto legibles de un archivo binario para encontrar la contraseña.

---

## Conceptos

- **Comando `strings`:** Extrae secuencias de caracteres imprimibles de archivos binarios. Muy útil para analizar archivos sin necesidad de abrirlos con un editor hexadecimal.
- **Archivos binarios:** A diferencia de los archivos de texto, los binarios contienen datos no legibles por humanos. `strings` permite encontrar texto incrustado.
- **Pipeline combinado:** `strings` + `grep` para filtrar solo las líneas relevantes.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **file** — Identificar tipo de archivo
- **strings** — Extraer texto de binarios
- **grep** — Filtrar líneas

---

## Comandos utilizados

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
ls
file data.txt
strings data.txt | grep "==="
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 9 (click para revelar)</summary>

`EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`
</details>

### Paso 2: Explorar

```bash
bandit9@bandit:~$ ls
```

**Resultado:** `data.txt`

```bash
bandit9@bandit:~$ file data.txt
```

**Resultado:** `data.txt: data`

Es un archivo binario. No se puede leer directamente con `cat`.

### Paso 3: Extraer texto del binario

Usé `strings` para extraer las cadenas de texto legibles:

```bash
bandit9@bandit:~$ strings data.txt | grep "==="
```

**Resultado:**
```
========== the
========== password
Y========== is
========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

La contraseña aparece después de los `=` en la última línea.

<details>
<summary>🔑 Contraseña obtenida para bandit10 (click para revelar)</summary>

`B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`
</details>

### Paso 4: Cerrar sesión

```bash
bandit9@bandit:~$ exit
```

---

## Resultado

Nivel 9 completado. Se usó `strings` para extraer texto legible de un archivo binario y `grep` para filtrar por el patrón de `=`.

---

## Lo que aprendí

- `strings` extrae cadenas imprimibles de archivos binarios (3 caracteres o más por defecto).
- `strings -n X` cambia la longitud mínima de las cadenas a mostrar.
- Combinar `strings` con `grep` permite buscar texto específico dentro de binarios.
- No todos los archivos se pueden leer con `cat`; `file` ayuda a identificar cómo abordarlos.
- `strings` es útil en análisis de malware, ingeniería inversa y CTFs.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man strings`
- `man grep`
- `man file`

---

## Notas

- `strings` puede usarse con binarios, core dumps, o cualquier archivo que pueda contener texto.
- El flag `-e` permite especificar la codificación (ASCII, UTF-16, etc.).
- En este nivel, las cadenas con `=` delimitaban el texto relevante.
