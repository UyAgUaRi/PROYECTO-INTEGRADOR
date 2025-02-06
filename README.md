<p align="center">
  <img src="https://github.com/user-attachments/assets/8d94fa85-31f0-4fe0-90d4-9afad8a5b7ca" width="20%" style="margin-right: 10px;" />
  <img src="https://github.com/user-attachments/assets/7f068076-91e3-4775-aa04-8256db3fa184" width="20%" />
</p>

<h1 align="center">Documentación de Servidores</h1>

> 🌟 *Integrantes:*  
> * Erick Uyaguari  
> erick.uyaguari@ucuenca.edu.ec  
> * Esteban Molina  
> esteban.molina@ucuenca.edu.ec  
> * Genaro Quezada  
> genaro.quezada@ucuenca.edu.ec  
> * Yadira Merchán  
> nataly.merchan@ucuenca.edu.ec  


INTRODUCCIÓN


### CREACIÓN DE UNA NUEVA MÁQUINA VIRTUAL
1. Abrir el software de virtualizacion: Inicie VirtualBox y haga click en "Nueva Maquina Virtual"

     **Asignamos Recursos**
      
     Nombre: Asignamos un nombre descriptivo, como "Servidor Centos" en este caso

     Tipo: Selccionamos "Linux"

     Version: Elegimos "Red Hat (64-bit)"

     Memoria RAM: Asignamos al menos 2GB (2048 MB)

     Disco Duro: Crea un disco virtual de al menos 20GB

     Montar la Imagen ISO: En la configuracion de la maquina virtual, seleccionamos la imagen ISO de CentOS descargada 
     previamente como medio de arranque

   <p align="center">
   <img src="https://github.com/user-attachments/assets/da30f6e1-60d7-45b0-aca5-7a9caa5ae063" alt="Imagen de instalación" width="80%">
</p>


     












### INSTALACIÓN DE SISTEMA OPERATIVO - CentOS 9 Stream
1. 








### INSTALACIÓN DEL SERVIDOR - SSH
1. Empezamos ejecutando el comando “sudo dnf install -y openssh-server” para instalar el servicio de ssh.
   
`sudo dnf install -y openssh-server`

<p align="center">
  <img src="https://github.com/user-attachments/assets/713117f6-4b29-4253-aefe-6f64cf2d3994" alt="Imagen de instalación" width="80%">
</p>


2. Seguido de la instalación agregamos el servicio de ssh al firewall.

`sudo firewall-cmd --permanent --add-service=ssh`

`sudo firewall-cmd --reload`
   
<p align="center">
   <img src="https://github.com/user-attachments/assets/89db1527-5dfd-4685-b9a4-a1cab7be229e" alt="Imagen de instalación" width="80%">
</p>


3. Continuamos agregando el puerto “54321” a la configuración del nano

`PORT 54321`

<p align="center">
   <img src="https://github.com/user-attachments/assets/d39b6840-63a5-4353-b1f8-09cf82e780d8" alt="Imagen de instalación" width="80%">
</p>


4. Para terminar agregamos el puerto “54321” a la configuración del firewall para evitar problemas de conectividad con el funcionamiento del servicio

`sudo firewall-cmd --permanent --add-port=54321/tcp`

`sudo firewall-cmd --reload`

<p align="center">
   <img src="https://github.com/user-attachments/assets/9f1496a9-d567-4b7e-af44-928bc3acd3be" alt="Imagen de instalación" width="80%">
</p>


5. Reiniciamos el servicio ssh para actualizar los cambios y que empiece su funcionamiento

`sudo systemctl restart sshd`

  <p align="center">
    <img src="https://github.com/user-attachments/assets/c1c57d55-e1e9-42c1-a475-c93a4debd205" alt="Imagen de instalación" width="80%">
    </p>

    
6. Conectamos el servicio

`ssh localhost -p 54321`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/96a17632-e6e8-4b8e-9397-48c2c9ed4bf7" alt="Imagen de instalación" width="80%">
   </p>


   7. Conexión remota con mobaxterm

   <p align="center">
<img src="https://github.com/user-attachments/assets/482a467e-ea29-4aff-bb31-11241c05710d" alt="Imagen de instalación" width="80%">
</p>



### INSTALACIÓN DEL SERVIDOR - SAMBA
1. 











### INSTALACIÓN DEL SERVIDOR - POSTFIX

1. Proceda a instalar el paquete de postfix

   `sudo dnf install postfix -y`

<p align="center">
   <img src="https://github.com/user-attachments/assets/2da7e2b7-4123-4366-a62e-6380704f90b5" alt="Imagen de instalación" width="80%">
</p>


2. Habilite como servicio predeterminado

   `sudo systemctl enable postfix`

   `sudo systemctl start postfix`

<p align="center">
   <img src="https://github.com/user-attachments/assets/97180813-f0c1-4300-af88-7ad805b6c8d5" alt="Imagen de instalación" width="80%">
   </p>


3. Empiece con la configración

      `sudo nano /etc/postfix/main.cf`

   <p align="center">
      <img src="https://github.com/user-attachments/assets/306b3aee-f751-48a1-aa8d-2f32e1796e29" alt="Imagen de instalación" width="80%">
      </p>
      
      <p align="center">
      <img src="https://github.com/user-attachments/assets/97a4ed85-9c8d-49a7-8c44-efda69ac599e" alt="Imagen de instalación" width="80%">
      </p>


4. Configure el firewall
   
`sudo firewall-cmd --permanent --add-service=smtp`

`sudo firewall-cmd --permanent --add-service=smtps`

`sudo firewall-cmd --reload`

<p align="center">
<img src="https://github.com/user-attachments/assets/80efab2b-8998-4b82-9258-2a526c6c36d3" alt="Imagen de instalación" width="80%">
</p>


5. Reinicie Postfix

   `sudo systemctl restart postfix`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/6c9daa4f-ff68-4746-90a9-b5710fbd4269" alt="Imagen de instalación" width="80%">
</p>


6. Verifique el estado
   
   `sudo systemctl status postfix.service`
   
<p align="center">
<img src="https://github.com/user-attachments/assets/c3cdcc4b-96cd-4cef-bf8a-8c080da97560" alt="Imagen de instalación" width="80%">
</p>


7. Pruebe el servicio (Instalar paquete si es necesario)

   `echo "Prueba de Postfix en CentOS 9" | mail -s "Correo de prueba" tuemail@dominio.com`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/70d140c9-3b6a-4c94-98d8-6ddbc1b56e05" alt="Imagen de instalación" width="80%">
   </p>


8. Revise cola de correos

      `sudo mailq`

      <p align="center">
      <img src="https://github.com/user-attachments/assets/cf7bdf73-56fc-462a-b887-4c72e7af00e2" alt="Imagen de instalación" width="80%">
      </p>


### INSTALACIÓN DEL SERVIDOR - PLEX
1. Descargue el plex, descargar el que esta subrayado

   <p align="center">
    <img src="https://github.com/user-attachments/assets/77a10fc6-f27b-4f2a-bd30-77c0c2e9fc39" alt="Imagen de instalación" width="80%">
    </p>

2. Abra la carpeta descargada e instalamos

   <p align="center">
     <img src="https://github.com/user-attachments/assets/dd2f660f-2a1a-4db5-9b94-655d564c90d5" alt="Imagen de instalación" width="80%">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/8aff06dc-709f-4ab1-9b58-ff5fb6bcf148" alt="Imagen de instalación" width="80%">
</p>

3. Active e inicie plex

   `sudo systemctl enable plexmediaserver.service`

   `sudo systemctl start plexmediaserver.service`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/74811c50-78b4-40c5-8317-f615fcecf96d" alt="Imagen de instalación" width="80%">
   </p>
   
4. Configure el firewall añadiendo el puerto "32400"

   `sudo firewall-cmd --add-port=32400/tcp --permanent`

   `sudo firewall-cmd -reload`

<p align="center">
<img src="https://github.com/user-attachments/assets/40a37ad1-0c3b-47c0-a4f6-409b4eace939" alt="Imagen de instalación" width="80%">
</p>

5. Acceda a plex desde el navegador usando "https://<ip-servidor-centos>:32400/web" (si no funciona con la ip del servidor) pruebe con esto "https://localhost:32400/web"

   <p align="center">
   <img src="https://github.com/user-attachments/assets/e0883ae8-c91f-4b83-8d29-436da4e1a0a3" alt="Imagen de instalación" width="80%">
   </p>

6. Configure plex, cree una cuenta

   <p align="center">
   <img src="https://github.com/user-attachments/assets/f0ae263d-c91e-41da-8c6b-8706e42fd936" alt="Imagen de instalación" width="80%">
      </p>

7. Una vez creada la cuenta proceda a darle un nombre a la empresa

   <p align="center">
   <img src="https://github.com/user-attachments/assets/fb3c3ff5-581e-4a41-a80c-1b69ac40f2ba" alt="Imagen de instalación" width="80%">
      </p>

8. Posteriormente de click en el nombre de la emprea para poder agregar bibliotecas

<p align="center">
   <img src="https://github.com/user-attachments/assets/d83ddc72-bae5-4fb8-aab8-10c0d92e7018"
 alt="Imagen de instalación" width="80%">
      </p>

9. Añada a la biblioteca

    <p align="center">
   <img src="https://github.com/user-attachments/assets/e990b19a-9353-4e52-ad46-f6e679dcdb80" alt="Imagen de instalación" width="80%">
      </p>

10. De un nombre a la carpeta y siguiente

  <p align="center">
   <img src="https://github.com/user-attachments/assets/52ae1835-e673-428f-9ba5-226715cd8ccb" alt="Imagen de instalación" width="80%">
      </p>

### INSTALACIÓN DEL SERVIDOR - DNS

1. Actualice
   
`sudo yum update -y`

2. Instale paquete bind

  `sudo yum install -y bind bind-utils`

3. Habilite DNS

`sudo systemctl enable named`

4. Configure firewall

   `sduo firewall-cmd --permanent --xone=public --add-service=dns`

5. Configure servidor DNS

   `sudo nano /etc/named.conf`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/e5e64f72-e7e1-4583-8e28-12644b0e8c3b"
 alt="Imagen de instalación" width="80%">
      </p>

6. Desactive las líenas "listen on" y "listen on v6" usando #

   <p align="center">
   <img src="https://github.com/user-attachments/assets/84f20caf-fd3b-446d-8db4-453e98f93c42" alt="Imagen de instalación" width="80%">
      </p>

7. Busque la líena "allow-query" y sustituye "localhost" por "any"

   <p align="center">
   <img src="https://github.com/user-attachments/assets/ecae5d1e-422b-478a-9471-71ab3c18d5e4" alt="Imagen de instalación" width="80%">
      </p>

8. Guarde los cambios y compruebe que no hay errores en la configuración

   `sudo named-checkconf`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/5836e06b-d657-4315-ab90-183a008d608f" alt="Imagen de instalación" width="80%">
      </p>

   si no se produce ninguna salida significa que todo esta correcto

9. Inicie el servidor

    `sudo systemctl start named`

     <p align="center">
   <img src="https://github.com/user-attachments/assets/565cfd6a-5b3e-4b0b-8192-b03f5dedbaee" alt="Imagen de instalación" width="80%">
      </p>

10. Verifique el estado
    
`sudo systemctl status named`
    
<p align="center">
   <img src="https://github.com/user-attachments/assets/b62a011d-1d62-4f00-8a87-3880d8fa7822"
 alt="Imagen de instalación" width="80%">
      </p>

11. Creamos un archivo de configuración adicionales

    `sudo nano /etc/NetworkManager/conf.d/10-dns.conf`

<p align="center">
   <img src="https://github.com/user-attachments/assets/8a8f8ae9-146f-4a17-be7f-f893efb62186"
alt="Imagen de instalación" width="80%">
      </p>

12. Recargue la configuracion

    `sudo systemctl reload NetworkManager`

<p align="center">
   <img src="https://github.com/user-attachments/assets/cde19e15-ed0e-48ac-949f-212aff12d525"
alt="Imagen de instalación" width="80%">
      </p>

13. Edite el siguiente archivo

    `sudo nano /etc/resolv/conf`

<p align="center">
   <img src="https://github.com/user-attachments/assets/3bc78086-a5b7-420b-aa62-291f2e89b33c"
alt="Imagen de instalación" width="80%">
      </p>

14. En la primera líena de nameserver agregue un #, guarde y cierre

<p align="center">
   <img src="https://github.com/user-attachments/assets/dc1269f6-4118-47f1-8dbc-29a20a7b855a"
alt="Imagen de instalación" width="80%">
      </p>

15. Treas gurdar los cambio y cerrar el archivo, ya puede probar la resolucion de nombres en cualquier maquina de red, con el comando "nslookup" y el domino de internet que prefiera

`nslookup kernel.org`

<p align="center">
   <img src="https://github.com/user-attachments/assets/a064f8df-9d65-4efc-9963-4213c2e67ef0"
alt="Imagen de instalación" width="80%">
      </p>
    
### INSTALACIÓN DEL SERVIDOR - ISSABEL
1. 






