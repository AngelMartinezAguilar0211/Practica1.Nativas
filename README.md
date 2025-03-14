# Práctica 1.- "Instalación y Funcionamiento de los Entornos Móviles"
 

# Sistema de Navegación Interior/Exterior ESCOM-IPN  

## Descripción General  

Este proyecto consiste en un juego para dispositivos Android, desarrollado en Kotlin, que simula un sistema de navegación en interiores de Unidad Profesional "Adolfo López Mateos" del Instituto Politécnico Nacional (IPN), con opciones para la Escuela Superior de Cómputo (ESCOM-IPN), Centro de Investigación en Computación (CIC), Centro De Innovación Y Desarrollo Tecnológico En Cómputo (CIDETEC), Escuela Superior de Ingeniería y Arquitectura (ESIA), Escuela Superior de Física y Matemáticas (ESFM); además lña navegacion exterior en la colonía Lindavista con los siguientes puntos de interacción: Plaza Vista Norte, Talleres Ticomán y el metro Indios Verdes. La aplicación permite a múltiples usuarios desplazarse en un mapa 2D, conectarse entre sí a través de Bluetooth y sincronizar su ubicación en tiempo real mediante un servidor WebSocket.  

Los jugadores pueden explorar distintos ubicaciones dentro de la delegación Gustavo A. Madero a través de un mapa en 2D, utilizando controles de movimiento, interactuar con áreas específicas para cambiar de ubicación y visualizar en tiempo real la posición de otros usuarios dentro del entorno virtual.  

## Arquitectura del Proyecto  

### Componentes Claves  

#### 📁 data.map/  
- **📁 Bluetooth/**  
  - **📄 BluetoothGameManager.kt**: Administra la lógica del juego para conexiones Bluetooth.  
- **📁 Game/**  
  - **📄 GameViewModel.kt**: ViewModel que gestiona el estado del juego.  
  - **📄 Player.kt**: Modelo de datos para los jugadores.  
- **📁 OnlineServer/**  
  - **📄 OnlineServerManager.kt**: Controla las conexiones con el servidor WebSocket.  
  - **📄 BluetoothWebSocketBridge.kt**: Funciona como un puente entre las conexiones Bluetooth y WebSocket.  

#### 📁 presentation.components/  
- **📁 MapActivities/**  
  - **📄 GameplayActivity.kt**: Activity principal que muestra el mapa del juego.  
  - **📄 BuildingNumber2.kt**: Representa la vista del segundo edificio.  
  - **📄 Salon2009.kt**: Activity para el salón 2009.  
  - **📄 Salon2010.kt**: Activity para el salón 2010.  
  - **📄 Cafeteria.kt**: Activity para la cafetería.
  - **📄 Zacatenco.kt**: Activity para el mapa de la Unidad Zacatenco del IPN.
  - **📄 Lindavista.kt**: Activity para la zona de lindavista norte.   
- **📁 ConnectionManagement/**  
  - **📄 BluetoothManager.kt**: Maneja las conexiones Bluetooth.  
  - **📄 ServerConnectionManager.kt**: Administra las conexiones al servidor.  
  - **📄 DeviceListActivity.kt**: Muestra la lista de dispositivos Bluetooth disponibles.  
- **📁 UI/**  
  - **📄 UIManager.kt**: Gestiona la interfaz de usuario.  
  - **📄 MovementManager.kt**: Controla el desplazamiento del jugador.  
- **📁 mapview/**  
  - **📄 MapGestureHandler.kt**: Maneja los gestos táctiles en el mapa.  
  - **📄 MapMatrixProvider.kt**: Gestiona la matriz de colisiones.  
  - **📄 MapRenderer.kt**: Se encarga del renderizado del mapa y sus elementos gráficos.  
  - **📄 MapState.kt**: Administra el estado del mapa (zoom, posición, etc.).  
  - **📄 MapView.kt**: Componente personalizado para la visualización del mapa.  
  - **📄 PlayerManager.kt**: Coordina la gestión de los jugadores en el mapa.  
- **📁 ui.theme/**  
  - **📄 MainActivity.kt**: Activity inicial, encargada de la pantalla de inicio.  

## Funcionalidades por Módulo  

### 1. data.map  
- **Bluetooth**: Administración de la conexión y comunicación mediante Bluetooth.  
- **Game**: Modelos de datos y lógica principal del juego.  
- **OnlineServer**: Manejo de conexiones con el servidor central.  

### 2. presentation.components  
- **MapActivities**: Implementación de los distintos mapas y edificios.  
- **ConnectionManagement**: Administración de conexiones en el juego.  
- **UI**: Gestión de la interfaz de usuario y controles.  
- **mapview**: Manejo de la representación gráfica del mapa.  
- **ui.theme**: Actividades de navegación principales.  

## Flujo de Navegación  

La navegación principal dentro del juego sigue la siguiente estructura:  

```
MainActivity → GameplayActivity → [BuildingNumber2, Cafeteria, etc.]
                  ↓                    ↓
                [Zacatenco]                 [Salon2009, Salon2010, etc.]
                  ↓
                [Lindavista]
```  

## Sistema de Mapas  

Cada edificio o área dentro del juego (GameplayActivity, BuildingNumber2, Salon2009, Salon2010, Cafeteria, Lindavista, Zacatenco) cuenta con:  
- Un diseño de interfaz específico en XML.  
- Su propia matriz de colisiones definida en MapMatrixProvider.  
- Puntos interactivos dentro del mapa (ESIA, ESFEM, CIC, CIDETEC).  
- Transiciones configuradas para desplazarse entre distintas áreas.

## Servidor y Sincronización  

Para garantizar la sincronización en tiempo real de la ubicación de los jugadores, el sistema se comunica con un servidor WebSocket, el cual está desarrollado en Node.js y Express.  

## Instrucciones de uso 
Al igual que el programa original, inicialmente se debe ingresar con un nombre de usuario a la aplicación.
Después de iniciar sesión el jugador aparecerá como un punto en el mapa y podrá moverse con los botones visibles a la izquierda en las direcciones cardinales. Los elementos con los que se puede interactuar se encuentran marcados con un ligero tono azul, igualmente cuando te encuentres en un punto en el cual se puede interactuar se mostrará un mensaje en la parte inferior de la pantalla.
Para interactuar con cualquier punto se deberá presionar el botón A estando sobre el punto con el cual se quiere interactuar. Y en caso de que no sea posible se avisará por medio de un mensaje.
Los mapas consisten en una cuadricula en la cual se avanza punto por punto hasta llegar al destino
Puntos de interés en la aplicación pueden abrir una aplicación distinta (Google, Maps) la cual no va a cerrar la aplicación, por lo que se podrá volver siempre al mapa original.



## Requisitos Técnicos  

- Android Studio.  
- Kotlin como lenguaje de programación.  
- Dispositivos Android con conectividad Bluetooth.  
- Servidor WebSocket (incluido en la carpeta Online-Server).  
