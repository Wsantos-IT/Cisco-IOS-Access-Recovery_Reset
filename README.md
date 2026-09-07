# Cisco-IOS-Access-Recovery_Reset
## **Lab01:** 
## - 🎯1 Recuperación de Acceso IOS en Router Cisco (Usuario y Contraseña Olvidados) 
## - 🎯2 Restablecimiento a configuracion de fabrica (Factory Reset)

  <img src="Lab01-imagen01.png" width="400">

##  Objetivo 1: Reestablecer la configuracion del router a fabrica usando Cisco IOS
  
1. Conectamos un cable de consola al puerto usb de nuestra portatil o PC y el otro extremo al puerto CONSOLE del router.
2. Ejecutamos un programa de terminal como PuTTy y colocamos las siguientes opciones:
   Connection Type: Serial
   Speed: 9600
   Serial Line: Abrimos dispositivos de windows y revisamos que puerto COM se ha asignado y se coloca por ejemplo "COM5"
   Si es Linux por ejemplo: /dev/ttyUSB0
3. Le damos a Open en el PuTTy
4. Encendemos el Router

   
<img src="Lab01-imagen02.png" width="300">       <img width="358" height="195" alt="Lab01-imagen03" src="Lab01-imagen03.png" />

5. Ejecutamos Comandos:
   ```
   Router>enable
   Router#erase startup-config
   Pulsamos Enter
   Router#reload
   ```

#### ✅ Objetivo 1 Completado: El Router se reiniciara con la configuracion de fabrica. 
-----------------------------------------------------------------------------------------
##  Objetivo 2: Recuperacion de acceso IOS en un Router Cisco
💡Necesitamos recuperar el acceso sin borar la configuracion.
Interrumpiremos el Boot del Router para acceder al modo ROMMOM y cambiar el confreg para poder acceder a la info del router y poder hacer cambios sin borrar nada.

<img width="546" height="294" alt="image" src="Lab01-imagen04.png" />


1. Con el Router apagado vamos a conectar el cable de consola y ejecutamos PuTTy como en el objetivo 1.
2. Al encender el router inmediatamente presionamos las teclas FN + B o en la ventana de la Terminal de PuTTy hacemos click derecho en el borde > Special Command > Break
   Ejecutamos repetidamente esta combinacion de teclas o click en el Special Command Break y accederemos al modo ROMMOM

   <img width="545" height="49" alt="image" src="Lab01-imagen05.png" />

3. Ejecutamos Comandos:
   ```
   rommon 1 >:confreg 0x2142
   rommon 1 >:reset
   ```
<img width="537" height="67" alt="image" src="Lab01-imagen06.png" />
Tecleamos "no" en este dialogo y enter

4. Ejecutamos Comandos por PASO 🚩:

   (Recupera la config antigua primero)
```
   Router#copy startup-config running-config   
```

💡En este punto revisamos contraseñas si no estan encriptadas y si no es el caso, recuperamos acceso creando otros usuarios
u otra clave enable.
```
   Router(config)#enable secret cisco

```
(cambiamos al register original antes de guardar la configuracion con la nueva clave)
```
   Router(config)#config-register 0x2102       
   Router(config)#copy running-config startup-config
   Router(config)#reload
```
#### ✅ Objetivo 2 Completado: Recuperamos el acceso del router sin borrar su configuracion.



