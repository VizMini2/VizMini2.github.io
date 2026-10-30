# Registro de cambios

Aquí se documentan todos los cambios relevantes de VizMini2.
El formato sigue Keep a Changelog y el proyecto usa versionado semántico (antes de la 1.0, las versiones menores aún pueden cambiar el comportamiento).

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
- Pestaña Bags: graba topics en archivos MCAP compatibles con `ros2 bag` y Foxglove, reprodúcelos en la red (0,5×, 1×, 2×, bucle), e importa, comparte y borra grabaciones.
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
