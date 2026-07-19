# Nivel 7 → Nivel 8

## Objetivo

Conectarse al nivel 7 de Bandit y encontrar la contraseña en un archivo de texto junto a la palabra "millionth".

---

## Conceptos

- **`grep`:** Busca patrones dentro del contenido de archivos. Es uno de los comandos más utilizados en Linux.
- **Pipeline (`|`):** Conecta la salida de un comando como entrada de otro.
- **Archivos grandes:** Cuando un archivo es muy extenso, buscar manualmente es inviable; herramientas como `grep` permiten filtrar rápidamente.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **file** — Identificar tipo de archivo
- **cat** — Leer archivos
- **grep** — Buscar texto en archivos

---

## Comandos utilizados

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
ls
file data.txt
cat data.txt | grep millionth
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 7 (click para revelar)</summary>

`Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`
</details>

### Paso 2: Explorar

```bash
bandit7@bandit:~$ ls
```

**Resultado:** `data.txt`

```bash
bandit7@bandit:~$ file data.txt
```

**Resultado:** `data.txt: Unicode text, UTF-8 text`

Un archivo de texto Unicode. Al abrirlo tiene muchas líneas.

### Paso 3: Buscar la palabra clave

El nivel indicaba que la contraseña estaba junto a la palabra "millionth". Usé `grep` con un pipeline:

```bash
bandit7@bandit:~$ cat data.txt | grep millionth
```

**Resultado:**
```
millionth    VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

La línea contiene "millionth" seguido de un tabulador y la contraseña.

> También se puede usar directamente `grep millionth data.txt` sin necesidad de `cat`.

<details>
<summary>🔑 Contraseña obtenida para bandit8 (click para revelar)</summary>

`VR1ljMayciFxbnUokuQmJFw6QC9VKtub`
</details>

### Paso 4: Cerrar sesión

```bash
bandit7@bandit:~$ exit
```

---

## Resultado

Nivel 7 completado. Se usó `grep` para filtrar la línea que contenía "millionth" dentro de un archivo de texto extenso.

---

## Lo que aprendí

- `grep` busca patrones de texto en archivos o en la entrada estándar.
- El pipeline `|` permite encadenar comandos: la salida de `cat` se convierte en la entrada de `grep`.
- `grep archivo` directamente también funciona: `grep millionth data.txt`.
- Para archivos grandes, `grep` es mucho más eficiente que leer todo el contenido manualmente.
- `grep` tiene muchas variantes: `grep -i` (insensible a mayúsculas), `grep -r` (recursivo), `grep -c` (contar).

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man grep`
- `man cat`
- `man file`

---

## Notas

- `grep` acepta expresiones regulares, lo que lo hace extremadamente flexible.
- Para buscar palabras completas se usa `grep -w`.
- El pipeline es uno de los conceptos más poderosos de Unix: permite combinar herramientas pequeñas para tareas complejas.
