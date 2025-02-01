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
### INSTALACIÓN DE SISTEMA OPERATIVO - CentOS 9 Stream
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


### INSTALACIÓN DEL SERVIDOR POSTFIX

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

      


