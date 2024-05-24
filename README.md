# Plataforma educativa para la implementación de algoritmos de robótica móvil en entornos reales y simulados
## Configuración del espacio de trabajo de la simulación
Para poder trabajar correctamente con el presente repositorio es necesario configurar un espacio de trabajo en la computadora del robot. Es necesario clonar este repositorio en tu máquina local. Sigue los pasos detallados a continuación para configurar de forma correcta al robot y a tu máquina local.

### Requisitos
* Sistema operativo Ubuntu 22.04
* Simulador Webots

### Instalación de ROS 2
Debes asegurarte de tener instalada la versión adecuada de ROS 2 tanto en la computadora del robot como en una máquina local. Se utilizó ROS 2 Humble LTS para el desarrollo de esta plataforma, dicha versión es compatible con Ubuntu 22.04. Las instrucciones detalladas de instalación se encuentran en la [Documentación de Humble](https://docs.ros.org/en/humble/Installation.html).

Se recomienda hacer una instalación completa de `ros-humble-desktop` para la máquina local y una instalación simplificada `ros-humble-ros-base` para la computadora del robot.

### Instalación de dependencias
Existen 2 dependencias principales para el correcto funcionamiento del robot:

#### Webots
Es necesario contar con el software Webots instalado para poder ejecutar correctamente este paquete. Se utilizó Webots r2023b para el desarrollo de esta simulación. Las instrucciones detalladas de encuentran en la [Documentación de Webots](https://cyberbotics.com/doc/guide/installing-webots)

#### URDF 2 Webots
Es necesario instalar esta librería de Python para correr correctamente la simulación
```bash
pip install urdf2webots
```

#### Webots ROS 2
Para instalar este paquete puede utilizar `apt-get`:
```bash
sudo apt-get install ros-humble-webots-ros2
```
O puede instalar desde la fuente usando el [repositorio de Cyberbotics](https://github.com/cyberbotics/webots_ros2).

### Creación del workspace
Debe abrir una terminal y ejecutar los siguientes comandos para crear el workspace del robot:
```bash
mkdir -p ~/simulation_ws/src
cd ~/simulation_ws/src
git clone https://github.com/cyberbotics/webots_ros2.git
cd ..
colcon build
source install/setup.bash
```

### Lanzamiento de la simulación
Para publicar todos los tópicos relacionados a la simulación del robot se debe ejecutar el comando:
```bash
ros2 launch webots_ros2_sparkle new_robot_launch.py
```
Debería abrir Webots con la vista del robot dentro del entorno simulado:
<img src="https://github.com/Hamed-Quenta/webots_ros2_sparkle/blob/main/images_sim/sim-prev.png" alt="Preview">
<p style="margin-top:10px; font-size: 16px;"><strong>Figura 1.</strong> Vista del robot dentro del entorno simulado.</p>
<br>

Debería ver los siguientes tópicos publicados:
2. `/cmd_vel`: Contiene las velocidades lineales y angulares de entrada del robot.
3. `/odom`: Contienen los datos de odometría de rueda de la simulación.
4. `/scan`: Contiene las lecturas del sensor LiDAR simulado publicadas a una frecuencia de 5.5Hz.
5. `/imu`: Contiene las lecturas de aceleración y orientación del sensor IMU simulado.
6. `/oak/rgb/image`: Contiene imágenes de la cámara RGB simulada.
8. `/tf`: Contiene las transformaciones de posición y orientación entre todos los links de la simulación.
9. `robot_description:`: Contiene información de los elementos visuales del robot simulado.

## Visualización de datos

<img src="https://github.com/Hamed-Quenta/webots_ros2_sparkle/blob/main/images_sim/sim-cam.png" alt="RGB">
<p style="margin-top:10px; font-size: 16px;"><strong>Figura 2.</strong> Lectura de datos de cámara RGB simulada.</p>
<br>
