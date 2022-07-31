# Práctica 25 - Uso de las reglas de seguridad

## Innovaccion Virtual (VII Edición) #IAWizards

### Semana 4 - Sesión 10

En esta práctica, se implementaron reglas de seguridad a una máquina virtual para poder conectar sus puertos y acceder a esta, así como también, se implementó una regla para quitarle el acceso a internet.

-------------------------------------------------------

#### Requerimientos
- Cuenta de Azure con suscripción. 
- [Microsoft Remote Desktop](https://apps.microsoft.com/store/detail/microsoft-remote-desktop/9WZDNCRFJ3PS?hl=en-us&gl=US).

--------------------------------------------------------

#### Pasos a seguir

1. Accedemos al portal de Azure y buscamos ‘Virtual Machines’ o ‘Máquinas Virtuales’ y creamos una. En la opción de ‘Puertos de entrada públicos’ le damos en ‘Ninguno’.

![P25I1](Images\Sesión 10 - P25 01.PNG)

2. En el apartado de ‘Redes’ de la VM vamos a la sección que diga ‘Grupo de seguridad de red de NC’ y la cambiamos a ‘Ninguno’.

![P25I2](Images\Sesión 10 - P25 02.PNG)

3. En el apartado de ‘Administración’ para el ‘Diagnostico de arranque’ le damos en ‘Deshabilitar’. Una vez habiendo hecho todo esto le damos en ‘Revisar y crear’.

![P25I3](Images\Sesión 10 - P25 03.PNG)

4. Una vez creada la VM, en el buscador de Azure buscamos ‘Grupos de seguridad de red’ y le damos en ‘Crear’. Una vez creado el recurso, ingresamos a este y en el apartado de ‘Interfaces de red’ le damos en ‘Asociar’ y asociamos la VM que creamos (Si no aparece, es porque deben estar en la misma región).

![P25I4](Images\Sesión 10 - P25 04.PNG)

![P25I5](Images\Sesión 10 - P25 05.PNG)

5. Regresamos a la VM en el apartado de ‘Conectar’, donde podremos descargar el RDP para ejecutarlo con ‘Escritorio Remoto’. Si lo hacemos, nos daremos cuenta de que no logra conectarse ya que se le ha quitado todos los puertos cuando lo creamos, para esto usaremos el grupo de seguridad.

![P25I6](Images\Sesión 10 - P25 06.PNG)

![P25I7](Images\Sesión 10 - P25 07.PNG)

6. Vamos al grupo de recursos de red y en el apartado de ‘Reglas de seguridad de entrada’ y le damos en ‘Agregar’. En la opción de ‘Servicio’ le ponemos ‘Custom’ y en ‘Intervalos de puertos de destino’ ponemos “3389” y en el apartado de ‘Protocolo’ ponemos ‘TCP’, mientras que en ‘Prioridad’ podemos poner “300”. Las demás configuraciones se pueden dejar por como estaban y al finalizar de configurar, le damos en ‘Agregar’.

![P25I8](Images\Sesión 10 - P25 08.PNG)

7. Una vez realizado el paso 6, volvemos a ejecutar el RDP con Escritorio Remoto y veremos que ya nos da acceso a la VM.

![P25I9](Images\Sesión 10 - P25 09.PNG)

8. Regresamos al grupo de seguridad de red y vamos al apartado de ‘Reglas de seguridad de salida’ y le damos en ‘Agregar’. En apartado de ‘Destino’ ponemos ‘Service Tag’, en ‘Servicio’ es ‘Custom’, en ‘Etiqueta’ ponemos ‘Internet’, en ‘Intervalos de puntos de destino’ ponemos “*”, en ‘Protocolo’ ponemos ‘TCP’, en ‘Acción’ le damos en ‘Denegar’ y en ‘Prioridad’ podemos poner “400”. Al finalizar le damos en ‘Agregar’. Podremos ver en la VM que ya no tiene acceso a internet, pues se le ha denegado con las reglas de seguridad.

![P25I10](Images\Sesión 10 - P25 10.PNG)

![P25I11](Images\Sesión 10 - P25 11.PNG)