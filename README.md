# Ejercicio 8

1. Crea un repositorio nuevo llamado **`ejer8_holamundo`**.  
2. Dentro, crea una carpeta llamada **`src`**.  
3. Añade un archivo con un programa en Java que muestre por la pantalla `“Hola”`.  
4. Haz una **`GitHub Action`** de manera que cuando se suba el programa a un repositorio remoto se ejecute automáticamente.

> **PISTA:** antes de ejecutar el programa, éste deberá ser compilado.


# `GitHub Action`

> Una `GitHub Action` es un flujo automatizado (workflow) que se ejecuta en los servidores de GitHub cuando ocurre un evento, como subir código.
- En mi caso, el evento es un push y el flujo debe compilar y ejecutar un programa Java.
## 1. Crea la carpeta de workflows

- En la raíz de tu repositorio (donde está .git), crea esta ruta:

```bash
.github/workflows/
```

## 2. Crea el archivo del flujo (por ejemplo `java.yml`)

En `.github/workflows/java.yml`, escribe esto:

```yaml
name: Compilar y ejecutar Java

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Descargar código del repositorio
        uses: actions/checkout@v4

      - name: Configurar Java
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Compilar el programa
        run: javac src/Hola.java

      - name: Ejecutar el programa
        run: java -cp src Hola
```

## 3. Subir el archivo al repositorio

Guarda y sube todo a GitHub:

```bash
git add .github/workflows/java.yml
git commit -m "Añadir GitHub Action para compilar y ejecutar Java"
git push

```

## 4. Comprobar que funciona

- Ir a repositorio en GitHub.

    - Entra en la pestaña `Actions`.

    - Verás un flujo llamado `Compilar y ejecutar Java` ejecutándose.

    - Si todo está correcto, en la salida aparecerá:

```bash
Hola

````
