# Checker de Dominios Activos

Un script de Bash simple pero potente para verificar rápidamente el estado de una lista de dominios o subdominios. Automatiza el proceso de validación para identificar qué objetivos web están activos y son accesibles, ahorrando un tiempo considerable durante las fases de reconocimiento en auditorías de seguridad o pentesting.

![Ejemplo de Salida del Script](/image/banner.jpg)  ## Características Principales

-   **Análisis Concurrente**: Utiliza `xargs` para realizar múltiples verificaciones en paralelo, acelerando significativamente el escaneo de listas grandes.
-   **Doble Protocolo**: Comprueba de forma inteligente tanto `https://` (preferido) como `http://` para cada dominio.
-   **Salida Informativa**: Muestra los códigos de estado HTTP (`2xx`, `3xx`, `4xx`) para los dominios activos, permitiendo una rápida interpretación.
-   **Visual y Claro**: Emplea códigos de color para diferenciar fácilmente los resultados:
    -   <span style="color:green">**Verde**</span> para respuestas exitosas (2xx).
    -   <span style="color:yellow">**Amarillo**</span> para redirecciones (3xx).
    -   <span style="color:red">**Rojo**</span> para errores de cliente interesantes como `401 Unauthorized` o `403 Forbidden`.
-   **Seguimiento de Redirecciones**: Sigue las redirecciones (códigos 3xx) y muestra la URL de destino final, lo cual es muy útil para entender el flujo de la aplicación.
-   **Ligero y Portable**: No requiere dependencias complejas, solo `bash` y `curl`, herramientas estándar en la mayoría de los sistemas operativos tipo Unix.

## Requisitos

-   Un sistema operativo tipo Unix (Linux, macOS, WSL en Windows).
-   **Bash** (Bourne Again SHell).
-   **cURL**.

## Instalación

1.  Clona este repositorio o descarga el script directamente:
    ```sh
    git clone https://github.com/4NTR4xX01/Check.git
    ```
2.  Navega al directorio del proyecto:
    ```sh
    cd Check
    ```
3.  Otorga permisos de ejecución al script:
    ```sh
    chmod +x check
    ```
4.  Mueve el archivo al directorio /usr/bin, para que lo ejecutes en cualquier lado de tu shell:
    ```sh
    sudo mv check /usr/bin
    ```

## Modo de Uso

1.  Crea un archivo de texto (ej. `lista.txt`) que contenga los dominios o subdominios que deseas verificar, uno por línea.

    **Ejemplo (`lista.txt`):**
    ```txt
    github.com
    gitlab.com
    un-dominio-que-no-existe.com
    google.com
    drive.google.com
    ```

2.  Ejecuta el script, pasándole como argumento la ruta a tu archivo de texto:
    ```sh
    check lista.txt
    ```

## Ejemplo de Salida

```
=============================================
        Check - by: 4NTR4xX
=============================================
Iniciando escaneo de dominios en: lista.txt
Procesos paralelos: 20 | Timeout: 10 segundos
---------------------------------------------
[200 OK] 	 [https://github.com](https://github.com)
[200 OK] 	 [https://gitlab.com](https://gitlab.com)
[301 REDIRECT] 	 [http://google.com](http://google.com) -> [https://www.google.com/](https://www.google.com/)
[200 OK] 	 [https://drive.google.com](https://drive.google.com)
---------------------------------------------
Escaneo completado.
=============================================
```

## Configuración

Puedes modificar fácilmente las siguientes variables al principio del script para ajustar su comportamiento a tus necesidades:

-   `MAX_JOBS`: Controla el número de procesos concurrentes. Un número más alto puede acelerar el escaneo, pero consume más recursos. El valor por defecto es `20`.
-   `TIMEOUT`: Define el tiempo máximo en segundos que `curl` esperará por una respuesta antes de rendirse. El valor por defecto es `10`.

## Autor

* **4NTR4xX**

## Licencia

Este proyecto es de código abierto. Siéntete libre de usarlo, modificarlo y distribuirlo. Se recomienda añadir una licencia como [MIT License](https://opensource.org/licenses/MIT).
