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
     ```
     ssh-copy-id usuario@ip_del_servidor
     ```
 En el segundo:
     ```
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


**Agregar la clave pública a la cuenta de GitHub:**
 Se accede a la configuración de SSH de la cuenta de GitHub en la página web de GitHub.
 En `Settings > SSH and GPG keys > New SSH key`, se pega el contenido de la clave pública en el campo proporcionado.

**Clonar el repositorio de GitHub:**
 Se utiliza el comando `git clone` para clonar el repositorio de GitHub que contiene el README que se desea autenticar en la máquina local.
     ```
     git clone git@github.com:usuario/repo.git
     ```

 **Editar y autenticar el README:**
 Se navega hasta el directorio del repositorio clonado y se edita el archivo README según las necesidades.
 Una vez realizados los cambios, se guarda el archivo.

 **Agregar, confirmar y empujar los cambios:**
 Se utilizan los comandos `git add`, `git commit` y `git push` para agregar, confirmar y empujar los cambios al repositorio remoto en GitHub.
     ```
     git add README.md
     git commit -m "Actualizar README con autenticación SSH"
     git push origin main
     ```
 Se asegura de reemplazar `main` con el nombre de la rama principal si es diferente en el repositorio.

Una vez completados estos pasos, el README estará autenticado con SSH en GitHub. Los cambios realizados se reflejarán en el repositorio remoto y estarán disponibles para otros usuarios.

