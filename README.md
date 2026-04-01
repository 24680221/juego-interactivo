# juego-interactivo

Este código se desarrolla un juego interactivo donde el usuario puede competir contra la máquina mediante una interfaz gráfica. Se combinan elementos visuales, eventos y lógica de programación para crear una aplicación dinámica y atractiva, demostrando cómo los componentes gráficos permiten una interacción sencilla y efectiva con el usuario.

Importación de librerías
-

- Flet → para crear la interfaz gráfica.
- random → para generar elecciones aleatorias de la máquina.
```
import flet as ft
import random
```

Función principal y configuracion de la ventana

Es el punto de entrada de la aplicación donde se construye toda la interfaz.ademas se define el titulo de la ventana, tamaño, color de fondo y espaciado interno.
```
def main(page: ft.Page):
    page.title = "Piedra, Papel o Tijeras"
    page.window_width = 400
    page.window_height = 600
    page.bgcolor = "#1e1e2f"
    page.padding = 20
```

aqui se definen las posibles juegadas, que usara la maquina y esta elija.
```
    opciones = {
        " Piedra": "Piedra",
        " Papel": "Papel",
        " Tijeras": "Tijeras",
    }
```

Componentes de texto
-

Estos elementos muestran:

- Elección del usuario
- Elección de la máquina
- Resultado del juego
```
    texto_usuario = ft.Text(size=18, color="white")
    texto_maquina = ft.Text(size=18, color="white")
    resultado = ft.Text(size=28, weight="bold")
```

Función del juego (evento principal)
-

Se ejecuta cuando el usuario presiona un botón.
``` def jugar(e):```

- Obtener elecciones
donde el usuario tiene su opcion seleccionada y la maquina la opcion aleatoria
```
        usuario = e.control.data
        maquina = random.choice(list(opciones.values()))    
```

-Mostrar elecciones
```
        texto_usuario.value = f"Tu elección: {usuario}"
        texto_maquina.value = f"Elección de la máquina: {maquina}"
```

- Lógica del juego
donde se evalua la opcion del usuaro y maquina, si da empate el texto sale amarrillo, vistoria verde y derrota de rojo
```
        if usuario == maquina:
            resultado.value = "¡Empate!"
            resultado.color = "yellow"

        elif (
            (usuario == "Piedra" and maquina == "Tijeras") or \
            (usuario == "Tijeras" and maquina == "Papel") or \
            (usuario == "Papel" and maquina == "Piedra")
        ):
            resultado.value = " ¡GANASTE!"
            resultado.color = "green"

        else:
            resultado.value = " PERDISTE"
            resultado.color = "red"
```

- Actualizar interfaz
Refresca la pantalla con los nuevos datos.
```     page.update()```


Tarjeta principal (contenedor visual)
-

Es el bloque donde se muestra la información. ```tarjeta = ft.Container( ```

- Contenido de la tarjeta
como el titulo, una linea divisora, y resultados.
```
        content=ft.Column(
            [
                ft.Text(
                    " PIEDRA, PAPEL O TIJERAS",
                    size=22,
                    weight="bold",
                    text_align="center",
                    color="white",
                ),
                ft.Divider(color="white"),
                texto_usuario,
                texto_maquina,
                resultado,
            ],
            horizontal_alignment=ft.CrossAxisAlignment.CENTER,
            spacing=15,
        ),
```

- Estilos
Fondo oscuro, Bordes redondeados, Sombra.
```
        bgcolor="#2a2a40",
        padding=20,
        border_radius=20,
        shadow=ft.BoxShadow(
            blur_radius=15,
            color="black",
            offset=ft.Offset(5, 5),
        ),
    )
```

Botones del juego
-

Se crean 3 botones:

- Piedra
- Papel
- Tijeras

Cada uno tiene:
la funcion onclick
```
    botones = ft.Row(
        [
            ft.ElevatedButton(" Piedra", on_click=jugar, data="Piedra", bgcolor="#3b82f6", color="white"),
            ft.ElevatedButton(" Papel", on_click=jugar, data="Papel", bgcolor="#10b981", color="white"),
            ft.ElevatedButton(" Tijeras", on_click=jugar, data="Tijeras", bgcolor="#ef4444", color="white"),
        ],
        alignment=ft.MainAxisAlignment.CENTER,
        spacing=10,
    )
```

Organización de la interfaz
-

Se agregan:

Tarjeta principal, Espacio, Botones.
```
    page.add(
        tarjeta,
        ft.Container(height=30),
        botones,
    )
```

Ejecución
-

Inicia la aplicación.
```
ft.app(target=main)
```

codigo completo
```
import flet as ft
import random


def main(page: ft.Page):
    page.title = "Piedra, Papel o Tijeras"
    page.window_width = 400
    page.window_height = 600
    page.bgcolor = "#1e1e2f"
    page.padding = 20

    opciones = {
        " Piedra": "Piedra",
        " Papel": "Papel",
        " Tijeras": "Tijeras",
    }

    texto_usuario = ft.Text(size=18, color="white")
    texto_maquina = ft.Text(size=18, color="white")
    resultado = ft.Text(size=28, weight="bold")

    def jugar(e):
        usuario = e.control.data
        maquina = random.choice(list(opciones.values()))    

        texto_usuario.value = f"Tu elección: {usuario}"
        texto_maquina.value = f"Elección de la máquina: {maquina}"

        if usuario == maquina:
            resultado.value = "¡Empate!"
            resultado.color = "yellow"

        elif (
            (usuario == "Piedra" and maquina == "Tijeras") or \
            (usuario == "Tijeras" and maquina == "Papel") or \
            (usuario == "Papel" and maquina == "Piedra")
        ):
            resultado.value = " ¡GANASTE!"
            resultado.color = "green"

        else:
            resultado.value = " PERDISTE"
            resultado.color = "red"

        page.update()

    tarjeta = ft.Container(
        content=ft.Column(
            [
                ft.Text(
                    " PIEDRA, PAPEL O TIJERAS",
                    size=22,
                    weight="bold",
                    text_align="center",
                    color="white",
                ),
                ft.Divider(color="white"),
                texto_usuario,
                texto_maquina,
                resultado,
            ],
            horizontal_alignment=ft.CrossAxisAlignment.CENTER,
            spacing=15,
        ),
        bgcolor="#2a2a40",
        padding=20,
        border_radius=20,
        shadow=ft.BoxShadow(
            blur_radius=15,
            color="black",
            offset=ft.Offset(5, 5),
        ),
    )

    botones = ft.Row(
        [
            ft.ElevatedButton(" Piedra", on_click=jugar, data="Piedra", bgcolor="#3b82f6", color="white"),
            ft.ElevatedButton(" Papel", on_click=jugar, data="Papel", bgcolor="#10b981", color="white"),
            ft.ElevatedButton(" Tijeras", on_click=jugar, data="Tijeras", bgcolor="#ef4444", color="white"),
        ],
        alignment=ft.MainAxisAlignment.CENTER,
        spacing=10,
    )

    page.add(
        tarjeta,
        ft.Container(height=30),
        botones,
    )


ft.app(target=main)
```
a continucion la ejecucion:

<img width="944" height="622" alt="image" src="https://github.com/user-attachments/assets/e1bd3ed9-5b43-42cd-84ba-fe3dd8ead951" />


<img width="836" height="459" alt="image" src="https://github.com/user-attachments/assets/b2d5db9b-eed0-4e6d-9ae6-e15988425c4a" />


<img width="875" height="480" alt="image" src="https://github.com/user-attachments/assets/612ea7ca-90da-4655-9ab5-e2fa0aacbcfe" />


<img width="757" height="442" alt="image" src="https://github.com/user-attachments/assets/b673a1df-3600-4fb3-babd-3e8b63da59fa" />


conversion de codigo a apk
-

La aplicación implementa una interfaz gráfica interactiva y lógica programada en Python, permitiendo su ejecución tanto en entorno de escritorio como en dispositivos móviles.

- herramientas utilizadas
    - Python
    - Flet
    - Flutter (para compilación)
    - Android SDK
- proceso de desarrollo

1.- Creación de la aplicación:
Se desarrolló la lógica de la app en Python usando Flety se diseñó la interfaz gráfica con componentes interactivos.

2.- Preparación del entorno:
Instalación de Flutter y Android SDK.
Verificación del entorno con flutter doctor.

3.- Generación del APK:
Se utilizó el comando: ```flet build apk```

Flet se encargó de:
Empaquetar la aplicación en Python
Generar los recursos (iconos, splash screen)
Compilar el proyecto con Flutter

4.- Solución de errores
Durante el proceso se presentaron problemas como:

    - Bloqueo de archivos por sincronización (OneDrive)
    - Rutas incorrectas del proyecto
    - Ubicación incorrecta del archivo main.py

Estos se resolvieron:

    - Moviendo el proyecto fuera de carpetas sincronizadas
    - Ejecutando los comandos en la carpeta correcta
    - Limpiando archivos temporales


- Resultado:

Se generó exitosamente un archivo: ```app-release.apk```

Ubicado en:```build/apk/```

Este archivo puede instalarse en dispositivos Android.

acontinuacion se muestra lo que se genra al finalizarse y lo que hace en el proceso:

<img width="1070" height="516" alt="Captura de pantalla 2026-02-28 230449" src="https://github.com/user-attachments/assets/58d121ac-9d56-46fe-881d-156b7fbbd82f" />

acontinuacion de la aplicacion generada:

![Screenshot_20260331_211126](https://github.com/user-attachments/assets/a2e2738d-19f1-4da0-a27a-33c4e33f68f6)
![Screenshot_20260331_211133](https://github.com/user-attachments/assets/8dc4cd27-fb81-45ff-9e95-08a3b6905136)


Conversion de codigo a pagina wed
-

Para convertir la aplicación en una página web, primero se desarrolló la interfaz y la lógica utilizando la librería Flet, la cual permite ejecutar aplicaciones en el navegador. Posteriormente, se generó una versión web del proyecto (build), donde el código se adapta para funcionar como aplicación web.

Una vez obtenidos los archivos necesarios (HTML, JavaScript y recursos), se realizó el despliegue en la plataforma Netlify mediante la opción de subir archivos (drag and drop). Este servicio permite alojar sitios web de forma sencilla y gratuita.

acontinuacion se muestra la ejecuicion

<img width="815" height="268" alt="image" src="https://github.com/user-attachments/assets/e1619a57-281d-465a-a84e-3c2d147ed82c" />

<img width="886" height="493" alt="image" src="https://github.com/user-attachments/assets/fcc417b8-46c1-4ba1-a083-f60bc8353114" />

<img width="880" height="528" alt="image" src="https://github.com/user-attachments/assets/11ae7213-88e1-4248-a305-884295fd3f9c" />
