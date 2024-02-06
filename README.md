# Conexión segura mediante claves pública y privada SSH

Para establecer una conexión segura a través del protocolo SSH utilizando claves pública y privada, se pueden seguir los siguientes pasos:

1. **Generar un par de claves SSH en la máquina local:**

 Se puede utilizar el comando `ssh-keygen` en la terminal para generar un par de claves RSA de 2048 bits.
     ```
     ssh-keygen -t rsa -b 2048 -f ~/ssh/holo
     ```
 Se debe seguir las indicaciones para seleccionar la ubicación predeterminada o personalizada para almacenar las claves, y opcionalmente, establecer una frase de contraseña para proteger la clave privada.

2. **Copiar la clave pública al servidor remoto:**
 Se puede utilizar `ssh-copy-id` o copiar manualmente el contenido de la clave pública (`~/.ssh/id_rsa.pub`) en el archivo `~/.ssh/authorized_keys` del usuario en el servidor remoto.

 En el primer caso:
     ```bash
     ssh-copy-id usuario@ip_del_servidor
     ```
 En el segundo:
     ```bash
     cat ~/.ssh/id_rsa.pub | ssh usuario@ip_del_servidor "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
     ```

3. **Autenticación con claves SSH:**
 Para iniciar sesión en el servidor remoto utilizando la clave privada, se debe ejecutar el siguiente comando:
     ```
     ssh usuario@ip_del_servidor
     ```
 Se debe proporcionar la frase de contraseña si se estableció al generar las claves.

4. **Desactivar la autenticación por contraseña en el servidor:**
 Para mejorar la seguridad, se puede desactivar la autenticación por contraseña en el servidor editando el archivo de configuración SSH (`/etc/ssh/sshd_config`) y estableciendo `PasswordAuthentication no`. Luego, se debe reiniciar el servicio SSH para aplicar los cambios.
     ```
     #Para ingresar
     sudo nano /etc/ssh/sshd_config 
     #Para reiniciar
     sudo service ssh restart
     ```

De esta manera, se podrá conectar al servidor remoto de forma segura utilizando claves SSH, sin necesidad de ingresar una contraseña.

# Transferencia de archivos utilizando FileZilla

Para transferir archivos de manera segura utilizando el cliente FileZilla, se pueden seguir estos pasos:

1. **Descargar e instalar FileZilla:**
   - Se debe descargar e instalar el cliente FileZilla desde su sitio web oficial según el sistema operativo utilizado.

2. **Configurar la conexión:**
   - Al abrir FileZilla y acceder a `Archivo > Gestor de sitios`, se puede crear un nuevo sitio y configurar la conexión con la información del servidor remoto, incluida la dirección IP, el puerto SSH (generalmente 22) y las credenciales del usuario.

3. **Seleccionar el protocolo de transferencia seguro:**
   - En la pestaña Protocolo, se debe seleccionar `SFTP - SSH File Transfer Protocol` para garantizar una conexión segura.

4. **Autenticación con claves SSH:**
   - En la pestaña Autenticación, se debe seleccionar `Clave de usuario` y especificar la ruta de la clave privada (generalmente `~/.ssh/id_rsa`).

5. **Conectar y transferir archivos:**
   - Al hacer clic en `Conectar`, se establecerá la conexión con el servidor remoto, permitiendo navegar y transferir archivos de manera segura entre la máquina local y el servidor remoto.

