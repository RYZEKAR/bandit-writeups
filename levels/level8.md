# Nivel 8 → Nivel 9

## Objetivo

Conectarse al nivel 8 de Bandit y encontrar la única línea que no se repite en un archivo de texto con muchas líneas duplicadas.

---

## Conceptos

- **`sort`:** Ordena las líneas de un archivo alfabéticamente. Necesario antes de `uniq` porque `uniq` solo detecta duplicados consecutivos.
- **`uniq -u`:** Imprime solo las líneas que son únicas (que aparecen exactamente una vez en el archivo).
- **Pipeline (`|`):** Combina `sort` y `uniq` para procesar el archivo en cadena.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **file** — Identificar tipo de archivo
- **sort** — Ordenar líneas
- **uniq** — Filtrar líneas repetidas

---

## Comandos utilizados

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
ls
file data.txt
sort data.txt | uniq -u
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 8 (click para revelar)</summary>

`VR1ljMayciFxbnUokuQmJFw6QC9VKtub`
</details>

### Paso 2: Explorar

```bash
bandit8@bandit:~$ ls
```

**Resultado:** `data.txt`

```bash
bandit8@bandit:~$ file data.txt
```

**Resultado:** `data.txt: ASCII text`

### Paso 3: Encontrar la línea única

El archivo contiene muchas líneas, algunas repetidas. Solo una línea es única. Para encontrarla:

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
```

**Resultado:**
```
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

- `sort` ordena todas las líneas para que las repetidas queden consecutivas.
- `uniq -u` filtra y muestra solo las líneas que aparecen exactamente una vez.

<details>
<summary>🔑 Contraseña obtenida para bandit9 (click para revelar)</summary>

`EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`
</details>

### Paso 4: Cerrar sesión

```bash
bandit8@bandit:~$ exit
```

---

## Resultado

Nivel 8 completado. Se combinó `sort` con `uniq -u` para encontrar la línea única entre muchas repetidas en el archivo.

---

## Lo que aprendí

- `uniq` solo elimina duplicados consecutivos, por eso siempre debe ir precedido de `sort`.
- `uniq -u` muestra solo las líneas que no tienen repetición.
- `uniq -d` hace lo opuesto: muestra solo las líneas que sí se repiten.
- `uniq -c` cuenta cuántas veces aparece cada línea.
- La combinación `sort | uniq` es un patrón clásico en Unix.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man sort`
- `man uniq`

---

## Notas

- Sin `sort`, `uniq` solo compararía líneas adyacentes, por lo que no detectaría duplicados separados.
- `sort -u` combina ordenar y eliminar duplicados en un solo comando, pero no permite el filtro de únicos (`-u` de `uniq`).
