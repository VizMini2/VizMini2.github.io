# Registro de cambios

Aquí se documentan todos los cambios relevantes de VizMini2.
El formato sigue Keep a Changelog y el proyecto usa versionado semántico.

## [1.1.0] - 2026-11-26

### Añadido
- **Actualizaciones con apt en Ubuntu:** VizMini2 tiene su propio repositorio de apt. Al instalar el `.deb` se añade una vez, así que `sudo apt upgrade` trae cada versión nueva; o añádelo a mano e instala con `sudo apt install vizmini2` (mira la instalación en Linux del manual).
- **El paquete de ROS 2 está listo para los repositorios de ROS** (`ros-<distro>-vizmini2`): el repositorio es el paquete, se compila como lo hace la buildfarm de ROS y se prueba en Jazzy y Lyrical en el CI (Jazzy o posterior: en Humble, el `.deb` es el camino). Funciona con el Java del sistema (17 o posterior) y ocupa menos: unos 55 MB, sin Java propio y sin el código de librerías que la app no usa.

### Cambiado
- **Descargas directas:** los botones del README y de la web descargan directamente el `.deb` y el `.msi` de la última versión (`vizmini2-linux-amd64.deb`, `vizmini2-windows-x86_64.msi`).
- **Compilar el paquete de ROS 2:** clona el repositorio en el `src` de tu workspace y ejecuta `colcon build` (`rosdep install` trae Java); `package.xml` está ahora en la raíz del repositorio en vez de en `ros/vizmini2`.

## [1.0.0] - 2026-11-25

### Añadido
- **VizMini2 para el PC (Linux y Windows):** las mismas pestañas que en el móvil, en una ventana. En Linux, instala el `.deb` en Ubuntu 20.04 o posterior, o compílalo como paquete de ROS 2 y arráncalo con `ros2 run vizmini2 vizmini2` (la primera vez toma el dominio y los peers de la terminal). También tiene el robot de demo (Configuración › Iniciar demo, o `vizmini2 --demo`), solo en ese ordenador.
- **En Windows 10 y 11** (64 bits): instala el `.msi` (para tu usuario, sin pedir administrador: te pregunta dónde y añade un acceso directo en el escritorio y en el menú Inicio) o descomprime el `.zip`. Al desinstalarla desde Configuración de Windows › Aplicaciones se conservan tus ajustes, bags y vídeos. El vídeo H.264/H.265 y la grabación de la ventana usan ffmpeg (`winget install ffmpeg`; si falta, la app explica cómo instalarlo), los diálogos de abrir y guardar son los de Windows, y un aviso indica cuándo se ha guardado un vídeo (al pulsarlo se abre el Explorador con él).
- **Pestaña MoveIt:** planifica y mueve un brazo robótico con `move_group`: grupos de planificación y poses con nombre, un slider por articulación, mover la pinza en X, Y, Z y alrededor de sus ejes, líneas rectas, el planificador y el tiempo de planificación, y obstáculos. Funciona con el MoveIt de Humble, Jazzy y posteriores.
- **Pestaña Controladores (ros2_control):** los controladores de un controller manager con su estado; actívalos, desactívalos, configúralos, cárgalos y descárgalos; mueve las articulaciones de los controladores de trayectorias y de comandos directos; y los componentes de hardware con sus interfaces. Foxy, Humble, Jazzy y posteriores.
- **Pestaña Mapas:** guarda el mapa en el robot (map_saver de Nav2 o SLAM Toolbox) o descárgalo en PGM y YAML, pausa SLAM, limpia los costmaps y dibuja zonas prohibidas y de límite de velocidad que se publican como máscaras de los filtros de costmap de Nav2.
- **Pestaña Alertas:** tus propias reglas sobre cualquier topic (un valor por encima o por debajo de un umbral, o unos segundos sin mensajes) con notificaciones, también en segundo plano, y los últimos avisos.
- **Pestaña PlanSys2:** sigue un plan de PlanSys2 mientras se ejecuta, como su monitor de terminal: el plan con el estado y el avance de cada acción, las acciones en curso y quién las hace, el conocimiento (instancias, predicados, funciones y el objetivo, con lo que ya se cumple) y el registro del plan, qué hace el ejecutor y por qué. Los cuatro juntos o cada uno por separado. PlanSys2 4.0.0 y posteriores (Jazzy, rolling) y los mensajes anteriores de la 3.x; el robot de la demo también tiene uno.
- **Topics de vídeo H.264 y H.265** (`foxglove_msgs/CompressedVideo` y ffmpeg_image_transport) en la pestaña Cámara y en los displays Image y Camera de la vista 3D. La cámara de la demo también se publica en H.264.
- **Graba la pantalla en vídeo:** el botón de grabar de arriba (se guarda en Movies/VizMini2); en el PC, Grabar vídeo en la barra lateral.
- **Importa y exporta** ficheros de RViz 2, layouts de paneles (`.json`) y layouts de gráficas (`.xml`), desde + y desde el menú de cada pestaña. Los paneles Publish pasan a ser botones, y cada pestaña de un layout llega como un dashboard propio.
- **Pestaña Gráficas:** series en el tiempo, XY, transiciones de estado, espectro e histograma, con fórmulas y scripts en Lua, desde topics, bags, ficheros CSV, UDP, MQTT y ZeroMQ.
- Pestañas **Indicadores, Mapa GPS, Árbol de comportamiento** (Groot2 con el blackboard, la grabación y los puntos de parada, y el log de Nav2), **Mensaje** y **Parámetros**.
- **Vista 3D:** displays Camera, DepthCloud, Effort, Image con anotaciones, Trajectory (la trayectoria planificada como robot fantasma) y Planning scene, marcadores de malla, marcadores interactivos, las herramientas Elegir, Medir y Publicar punto, y una herramienta de MoveIt para arrastrar el objetivo del brazo. Los paneles de imagen y de cámara se pueden mover y redimensionar.
- **Display NavMap:** los mapas NavMap de EasyNavigation (`navmap_ros_interfaces/NavMap`) en la vista 3D: superficies navegables en una o varias plantas, coloreadas por cualquiera de sus capas (coste, elevación, ocupación…), con los enlaces entre plantas (escaleras, ascensores, puertas) y las actualizaciones de capas en directo. Los ficheros de RViz con su plugin se importan y se exportan.
- **Fixed frame escrito a mano:** en la pestaña RViz, escribe cualquier frame, aunque aún no esté en TF, para dejar una vista preparada; mientras no aparezca se usa el automático.
- **Robots con rmw_zenoh_cpp** (router de Zenoh en Ajustes › Red), y servicios, acciones, parámetros y lifecycle de nodos con rmw_cyclonedds_cpp.
- **A través de foxglove_bridge:** topics, servicios, parámetros, acciones y el grafo de nodos.
- **Buscar robots** (Ajustes › Red) muestra los dominios de ROS con nodos en la red; toca uno para conectarte.
- **Variables de los topics:** escribe `${nombre}` en cualquier topic y pon su valor una vez en Ajustes, para cambiar todas las pestañas a otro robot de golpe.
- **Bags:** reproducción directa con una línea de tiempo común para todas las pestañas.
- **Pestañas:** duplícalas, compártelas como fichero e impórtalas (en el PC, con clic derecho en una pestaña la renombras, la duplicas, la borras o la exportas). Los widgets del dashboard se quedan donde los sueltas y pueden solaparse (un joystick sobre la vista 3D), y los de cámara y joystick son más compactos.
- **Tipos de mensaje que la app no trae:** pega su definición (lo que muestra `ros2 interface show`) justo donde la necesitas, desde las pestañas Topics, Mensaje, Services y Actions o desde cualquier lista de tipos, y úsalos al momento.
- La pestaña Cámara enseña hasta cuatro cámaras, con sus anotaciones.
- La pestaña Nodos enseña el DDS de cada nodo.
- El robot de la demo tiene un controller manager de ros2_control (si desactivas su diff_drive_controller, se para) y su cámara también como vídeo H.264.

### Cambiado
- **Ya no hace falta cuenta:** la app se abre directamente en Inicio y se conecta a tus robots sin ella; una cuenta (Google, Microsoft o GitHub) solo sincroniza tus perfiles de robot entre dispositivos.
- VizMini2 es software libre con la Apache License 2.0.
- Nuevo icono y logo de la app, en el móvil y en el PC.
- La app usa como objetivo Android 16 (API 36).
- Botones: una lista larga en un resultado muestra sus primeros valores y cuántos hay (`[0, 1, 1, 2, 3, 5, …] (11)`) en vez de solo `[11]`.
- Bags: las estadísticas de la grabación y la posición de la reproducción se actualizan mientras están en marcha.
- PC: las pestañas de la barra lateral se encogen para caber en una ventana pequeña y, si hay más, aparece una barra de desplazamiento.
- PC: Grabar vídeo y Ctrl+Mayús+R avisan si falta ffmpeg y explican cómo instalarlo, y ffmpeg también se encuentra donde lo dejan winget y las instalaciones habituales.
- PC: los diálogos de abrir y guardar tienen título y solo muestran el tipo de fichero que toca, y se añade la extensión si escribes un nombre sin ella.
- PC: los instaladores pesan unos 40 MB menos (cada uno lleva solo las librerías nativas de su sistema).
- Línea de comandos del PC: `--tab` acepta también el nombre de una pestaña, e `--import` abre la pestaña importada.
- Los modos de control de la teleoperación y los botones del panel de displays de RViz en el PC (Añadir, Duplicar, Quitar, Renombrar, Color de fondo) están traducidos.

### Corregido
- Servicios: varias llamadas a la vez al mismo servicio (también los resultados de las acciones) reciben cada una su propia respuesta, aunque el servidor conteste en otro orden; y los clientes de ROS 2 con Fast DDS, como `ros2 service call`, pueden usar los servicios que ofrece la app (los del robot de la demo).
- PC: cualquier clic en una pestaña Teleop (como Conducir, de la demo) le devuelve el teclado después de que se lo quitaran la barra lateral o un diálogo.
- PC: en Windows, las mallas del robot también se encuentran en la instalación local de ROS 2 (`AMENT_PREFIX_PATH`).
- PC: la app ya no crea una carpeta `.ihmc` en tu carpeta personal.
- Cierres al arrancar en Android 12 y 13, en Android 8 y 9, y al girar el móvil en horizontal en RViz o Cámara.
- Con un bag en bucle o una simulación reiniciada, la vista 3D se quedaba congelada: el historial de TF se vacía cuando el tiempo salta hacia atrás, como en RViz.
- Bags: cambiar la velocidad de reproducción hacía que los mensajes llegaran a golpes o se pararan, y algunos ficheros podían bloquear el lector.
- Al entrar con otra cuenta, los perfiles de la anterior se subían a la nueva.
- Una malla usada por dos displays a la vez no se veía en el segundo, y una gráfica podía bloquear la app con valores muy grandes.
- Dos partes de la app publicando a la vez en el mismo topic podían mandar un mensaje dos veces, y los botones de los marcadores interactivos podían perder un clic.
- El robot de la demo nunca llegaba a pararse del todo (su velocidad oscilaba).

## [0.18.0] - 2026-10-11

### Añadido
- Si guardas, borras o sincronizas perfiles sin conexión a internet, la app te avisa. Los cambios se quedan guardados en el móvil y se suben solos a la nube en cuanto vuelves a tener conexión; mientras tanto, la tarjeta de perfiles de Ajustes indica que hay cambios pendientes.

### Cambiado
- Con la sesión iniciada puedes abrir la app y usar tus robots sin conexión a internet, por ejemplo conectado solo a la Wi-Fi del robot, y ahora entra al momento sin esperar al servidor. Ese uso sin conexión caduca: pasado un tiempo, la app te pide conectarte a internet un momento para comprobar tu cuenta (sin volver a escribir la contraseña) y después puedes seguir sin conexión.

### Corregido
- Al abrir la app sin conexión a internet, a veces se cerraba la sesión y había que volver a entrar cuando hubiera conexión.
- Si la cuenta se eliminaba desde otro móvil, este seguía entrando con la sesión guardada; ahora pide volver a iniciar sesión.
- Sincronizar los perfiles sin conexión se quedaba en "sincronizando…" indefinidamente.

## [0.17.1] - 2026-10-10

### Corregido
- Al entrar con Microsoft o GitHub, la app podía quedarse en la pantalla de inicio de sesión con el indicador de carga girando sin pasar nunca a la pantalla principal; había que cerrarla y volver a abrirla para que reconociera la sesión. Ya entra directamente al terminar en la página de Microsoft o GitHub. El mismo problema afectaba a vincular esas cuentas desde Inicio y a confirmar el borrado de la cuenta volviendo a entrar con ellas, y también queda corregido. (Con Google no pasaba.)

## [0.17.0] - 2026-10-10

### Añadido
- Entra o regístrate con Google, Microsoft o GitHub, sin tener que crear otra contraseña. La primera vez se crea tu cuenta con el nombre y el correo que da el proveedor, sin pasar por la verificación por correo.
- Vincula desde Inicio varias formas de entrar a la misma cuenta. En la tarjeta de tu cuenta aparecen tus formas de entrar (correo y contraseña, Google, Microsoft y GitHub), cada una con un botón para vincularla o desvincularla; así, aunque un día entres con Google y otro con Microsoft, llegas siempre a la misma cuenta con tus mismos perfiles. La última forma de entrar que quede no se puede quitar, para no dejarte fuera de tu cuenta.
- Si intentas entrar con un proveedor cuyo correo ya tiene una cuenta, la app te avisa y te explica que entres como la primera vez y vincules el nuevo método desde Inicio.

### Cambiado
- Los botones de Google, Microsoft y GitHub están tanto en la pantalla de inicio de sesión como en la de registro.
- Los correos de verificación y de cambio de contraseña llegan en el idioma con el que estás usando la app.
- Al eliminar la cuenta, si entraste con Google, Microsoft o GitHub se confirma volviendo a entrar con ese servicio (antes solo con la contraseña).

## [0.16.0] - 2026-10-09

### Añadido
- Prueba la demo sin cuenta, directamente desde la pantalla de inicio de sesión. Inicio explica lo que estás viendo y cómo crear una cuenta para llegar a tus robots reales.
- El robot de la demo tiene parámetros, servicios (volver a la base, piloto automático, sumar dos enteros), una acción Fibonacci y un driver de cámara lifecycle, así que Nodos, Services, Actions, Lifecycle, Botones y Grafo de nodos se pueden probar sin un robot real. La demo incluye pestañas de Botones y Lifecycle listas para usar.
- El catálogo "+" muestra un vídeo corto en bucle de cada tipo de pestaña funcionando con el robot de la demo, en inglés o en español.
- Web de documentación con todas las funciones, vídeos y tutoriales, en español e inglés, desde Inicio.
- Política de privacidad en español e inglés, desde el inicio de sesión, el registro e Inicio.
- Elimina tu cuenta desde Inicio: se borran tu cuenta, tu nombre, tu correo y tus perfiles en la nube (se pide la contraseña para confirmar).
- Contacto y errores desde Inicio: un correo con la versión de la app, la de Android y el modelo del móvil ya rellenados.
- Apoya el proyecto desde Inicio, a través de GitHub Sponsors.

### Cambiado
- El registro pide nombre, apellidos, correo y la contraseña dos veces, y puedes entrar en cuanto confirmas tu correo.
- Los tipos de pestaña están traducidos en el catálogo "+", en Inicio y en los nombres de las pestañas nuevas (Cámara, Diagnóstico, Árbol TF…). También las pestañas de la demo.
- Sin cuenta, la app solo puede llegar al robot de la demo: los ajustes de red y los perfiles de robot se ocultan, y la conexión nunca sale del móvil.
- El recorrido rápido y la política de privacidad tienen su propia tarjeta en Inicio, debajo de Novedades.

### Corregido
- Una llamada a un servicio podía esperar hasta agotar el tiempo cuando el servidor respondía muy rápido sin identidad de la petición.

## [0.15.0] - 2026-10-06

### Añadido
- Traducción al español, incluido este registro de cambios. Elige el idioma en Ajustes (English, Español o el del sistema).

### Cambiado
- Ajustes está más ordenado: el estado de la conexión está en la tarjeta Red (Inicio mantiene el botón de reconectar) y el registro de cambios queda solo en Inicio.
- La visita guiada pasa de Inicio a Ajustes, y desaparece el consejo del día de Inicio.
- Builds de release más pequeñas y optimizadas.

## [0.14.0] - 2026-10-02

### Añadido
- La visita guiada incluye los dashboards, el grafo de nodos, el árbol de TF y la comprobación de red, con capturas nuevas.

### Cambiado
- Node graph también muestra los participantes que no anuncian nombres de nodo ROS, con su nombre de participante DDS (incluido el robot de demo).
- Capturas nuevas en el catálogo "+".

### Corregido
- Los robots recordados podían tomar el nombre de un nodo auxiliar oculto (como el daemon del CLI de ros2).
- Las etiquetas del joystick se solapaban en los widgets pequeños del dashboard.

## [0.13.0] - 2026-09-29

### Añadido
- Pestaña Dashboard: crea tu propia pantalla con cualquier pestaña como widget (vista 3D, varias cámaras, joystick, botones, diagnósticos…). Muévelos arrastrando, cámbialos de tamaño desde la esquina y quítalos en modo edición; se ajustan a una cuadrícula y nunca se solapan.
- La demo incluye un dashboard ya preparado.
- Node graph y TF tree ahora también son pestañas: añádelas desde "+" o ponlas en un dashboard.
- Recordar robots en esta red: la próxima vez se conecta directamente con los robots que la app ya ha visto, aunque el Wi-Fi descarte el tráfico multicast.
- Comprobación de red en Ajustes: qué ve el móvil en la red y qué hacer cuando el robot no aparece.
- Ya se pueden abrir y reproducir bags comprimidos con zstd (el valor por defecto en muchas instalaciones de ROS 2).
- Los informes de fallos también cubren los cierres dentro del código nativo.

### Cambiado
- Un cliente de service puede lanzar varias llamadas a la vez, y un cliente de action varios goals, cada uno con su propio feedback.
- Los botones de teleop se adaptan a espacios pequeños.

### Corregido
- La hora de sincronización con la nube se mostraba en el idioma del móvil en lugar del de la app.

## [0.12.0] - 2026-09-24

### Añadido
- Pestañas Nodes, Topics, Services y Actions: explora todo lo que hay en la red, como con el CLI de ros2.
- Pantalla de topic con echo en directo, frecuencia (Hz) y los nodos que publican y se suscriben a él.
- Llama a cualquier service desde un formulario de petición y envía goals de action con feedback en directo, resultado y cancelación.
- Nuevo catálogo "Añadir pestaña": cada tipo de pestaña con una breve descripción y una vista previa, y una página de configuración antes de crearla.
- Visita guiada para nuevos usuarios, disponible desde Inicio en cualquier momento.
- Modo demo: un robot simulado se ejecuta en el móvil (TF, mapa, láser, cámara, diagnósticos) y se puede manejar con teleop. Tu configuración vuelve al salir.
- Informes de fallos, para corregir los problemas más rápido.

### Cambiado
- El botón "+" abre el nuevo catálogo en lugar de una lista.
- Textos de la interfaz preparados para las próximas traducciones.

### Corregido
- La configuración de la pestaña Camera ahora sugiere los topics de imagen encontrados en la red.
- Los mensajes de imagen grandes se publican con mucha menos sobrecarga.

## [0.11.0] - 2026-09-19

### Añadido
- Pestaña Bags: graba topics en archivos MCAP compatibles con `ros2 bag`, reprodúcelos en la red (0,5×, 1×, 2×, bucle), e importa, comparte y borra grabaciones.
- Inspector de nodos: parámetros de cualquier nodo, editables como con `ros2 param` (todos los tipos, rangos y marcas de solo lectura), además de lo que publica, a lo que se suscribe y los services que ofrece.
- Grafo de red: nodos y topics como en `rqt_graph`, con búsqueda y filtros, y un árbol de TF en directo como `rqt_tf_tree`.
- Número de nodos en Inicio; toca un nodo para abrirlo en el inspector.
- Alertas del robot: notificaciones cuando se pierde el contacto con el robot, un diagnóstico pasa a ERROR o STALE, o un nodo lifecycle desaparece, se apaga o falla.
- Perfiles en la nube: los perfiles de robot se guardan en tu cuenta y aparecen en cualquier móvil en el que inicies sesión.
- Comparte un perfil como código QR (perfil completo o solo la conexión) e importa uno escaneándolo.
- Soporte para Discovery Server, como `ROS_DISCOVERY_SERVER`, para redes grandes, 4G o VPN.

### Cambiado
- Las tarjetas de Lifecycle pueden abrir los parámetros del nodo.
- Al grabar `/tf_static`, `/map` y `robot_description` se mantiene su comportamiento latched (transient local).

### Corregido
- El texto con tildes o "ñ" en parámetros y estados lifecycle se mostraba con caracteres extraños.
- La primera llamada a un service justo después de conectar podía fallar con "does not publish responses".

## [0.10.0] - 2026-09-14

### Añadido
- Nuevo icono de la app, con una variante temática (monocromo) para Android 13 y posteriores.
- Indicador de conexión en la barra superior de cada pestaña; tócalo para abrir Ajustes.
- Sección Acerca de en Ajustes con la versión de la app y el registro de cambios.

### Cambiado
- Ajustes rediseñado en tarjetas, a juego con la pestaña Inicio.
- Aspecto coherente en todas las pestañas: tarjetas y campos redondeados, iconos de pestaña y franjas de estado en Buttons, Lifecycle y Diagnostics.
- La imagen de la cámara se muestra en un marco redondeado y la búsqueda de topics está más a mano.

### Corregido
- Los peers de descubrimiento solo llegaban a los cuatro primeros procesos ROS de cada peer, así que los nodos lanzados después podían quedar invisibles.

## [0.9.0] - 2026-09-09

### Añadido
- Pestaña Inicio con pantalla de bienvenida, resumen de la conexión en directo, vista general del grafo ROS y novedades.
- Pestaña Lifecycle: descubre los nodos gestionados en la red, consulta su estado actual en directo y lanza transiciones (configure, activate, deactivate, cleanup, shutdown).
- Descubrimiento del grafo ROS en directo: los topics, services y actions se listan directamente desde el descubrimiento DDS, como `ros2 topic list`, `ros2 service list` y `ros2 action list`.
- Selectores de service y action en el editor de botones, rellenados desde el grafo descubierto con sus tipos.
- Visor completo del registro de cambios, accesible desde la pestaña Inicio.
- Versión de la app visible en la pantalla de inicio de sesión y en Inicio.
- "¿Has olvidado tu contraseña?" en la pantalla de inicio de sesión.
- Ajuste de peers de descubrimiento (como `ROS_STATIC_PEERS`) para redes Wi-Fi que descartan el tráfico multicast.

### Cambiado
- La interfaz se unifica en inglés, incluidos los nombres por defecto de las pestañas existentes.
- Pantallas de inicio de sesión y registro rediseñadas.
- Inicio y Ajustes son ahora pestañas fijas; cerrar sesión pasa de Ajustes a Inicio.
- La búsqueda de topics en las pestañas RViz y Camera lista todos los topics de la red en lugar de probar un conjunto fijo de nombres.

### Corregido
- La búsqueda de topics podía pasar por alto topics con nombres o tipos poco habituales.
- Las respuestas de los services ahora se asocian a su petición, así que dos clientes que llaman al mismo service ya no ven las respuestas del otro.

## [0.8.2] - 2026-09-03

### Corregido
- Los caracteres no ASCII (tildes, ñ) en los logs de `/rosout` y en los diagnósticos se mostraban con caracteres extraños.
- Algunos suscriptores rechazaban los mensajes `std_msgs/Empty` publicados desde un botón.
- Girar el dispositivo mientras se cargaba la vista 3D podía congelar la app unos segundos.

## [0.8.1] - 2026-09-01

### Corregido
- Los botones de action se quedaban en "En ejecución…" si el servidor de action desaparecía a mitad de un goal.
- Las respuestas largas de los services se cortaban en el diálogo de resultado.
- La cuadrícula de botones perdía la posición de desplazamiento al volver a la pestaña.

## [0.8.0] - 2026-08-28

### Añadido
- Pestaña Buttons: botones configurables que publican un mensaje, llaman a un service o envían un goal de action, con feedback y cancelación.
- Editor de formularios para cualquier tipo de mensaje, con soporte para campos anidados y arrays.
- Definiciones personalizadas de mensajes, services y actions para paquetes no incluidos en la app.
- Publicación repetida mientras mantienes pulsado, a una frecuencia configurable.

### Cambiado
- Diagnostics: en el selector de gráficas solo se ofrecen los topics que se pueden representar.

## [0.7.0] - 2026-08-19

### Añadido
- Perfiles de robot: guarda los ajustes de conexión y todas las pestañas con un nombre y cambia de robot con un toque.
- Importa y exporta perfiles como archivos JSON para compartirlos con tu equipo.
- Modo en segundo plano opcional que mantiene vivo el nodo ROS 2 con una notificación.

### Corregido
- Cambiar el Domain ID no siempre eliminaba las suscripciones antiguas.

## [0.6.1] - 2026-08-11

### Corregido
- Soporte para dispositivos con páginas de memoria de 16 KB (Android 15 y posteriores).
- Cierre inesperado al volver a abrir una pestaña de cámara tras cambiar su topic.
- Los ajustes de teleop no se guardaban al cerrar la app desde la pantalla de recientes.

## [0.6.0] - 2026-08-06

### Añadido
- Pestaña Diagnostics: resumen de `/diagnostics` agrupado por nivel, echo de topics con filtro de campos y gráficas en directo de los campos numéricos.
- Visor de logs de `/rosout` con filtro por nivel.
- Soporte para mandos físicos en las pestañas de teleop.

### Cambiado
- Teleop: parada de seguridad cuando se pierde la red, se desconecta el mando o la interfaz deja de responder.

## [0.5.0] - 2026-07-27

### Añadido
- Importa archivos de configuración `.rviz`: se restauran los displays compatibles, el fixed frame y la vista.
- Display Robot Model con mallas (STL, DAE) servidas por HTTP desde el robot.
- Displays Marker y MarkerArray, incluido texto.
- Vistas orbital, cenital y en primera persona.

### Corregido
- Los frames de TF podían parpadear cuando transformadas estáticas y dinámicas compartían padre.

## [0.4.0] - 2026-07-14

### Añadido
- Pestaña Teleop con un joystick en pantalla que publica `geometry_msgs/Twist`.
- Teleop con doble joystick para robots holonómicos y drones.
- Velocidades predefinidas e inversión por eje.

## [0.3.0] - 2026-07-03

### Añadido
- Pestaña Camera para `sensor_msgs/Image` y `CompressedImage`, con búsqueda automática de topics.
- Displays Map, Path, Pose y PoseArray.
- Display PointCloud2 con coloreado por intensidad y RGB.

### Cambiado
- Renderizado 3D más fluido con un nuevo renderizador de base física.

## [0.2.0] - 2026-06-23

### Añadido
- Pestañas: crea, renombra y borra tus propias pestañas RViz.
- Pestaña Ajustes con Domain ID, nombre del nodo y selección de interfaz de red.
- Display LaserScan y ejes de los frames de TF.

### Corregido
- La app no se reconectaba tras cambiar de red Wi-Fi.

## [0.1.0] - 2026-06-12

### Añadido
- Primera build interna.
- Inicio de sesión y registro con verificación por email.
- Vista 3D con cuadrícula y selección del fixed frame.
- Conexión a ROS 2 mediante DDS en la red local.
