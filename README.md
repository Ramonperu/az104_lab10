# LAB 10 - Copia de seguridad de máquinas virtuales

Enero 17 de 2023*, Ramón Peinado Ruiz

Vamos a aprender a usar las copias de seguridad de las maquinas virtuales

**Objetivos:**

------

• Task 1: Aprovisionar el entorno de laboratorio. 

• Task 2: Crear una bóveda de servicios de recuperación.

• Task 3: Implementar copia de seguridad a nivel de máquina virtual de Azure.

• Task 4: Implementar copia de seguridad de archivos y carpetas. 

• Task 5: Recuperación de archivos mediante el agente de Azure Recovery Services.

• Task 6: Recuperación de archivos mediante el uso de instantáneas de máquinas virtuales de Azure.

• Task 7: Revisar la funcionalidad de eliminación temporal de Azure Recovery Services.

**Diagrama:**

------

<img src="/img/1ºimagenn.png" alt="1ºimagenn" style="zoom:80%;" />

### TASK 1:

------

Hemos de comenzar subiendo las templates al shell 

<img src="/img/2ºimagenn.png" alt="1ºimagenn" style="zoom:80%;" />

Comprobamos que están subidos los  archivos con las plantillas, tras esto declaramos las variables correspondientes a nuestra localización y nombre de grupo, para la creación de nuestro grupo de recursos, una vez creado hacemos el despliegue de nuestras templates

<img src="/img/4ºimagenn.png" alt="4ºimagenn" style="zoom:80%;" />

### TASK 2:

------

Creamos la bóveda de servicios de recuperación:

<img src="/img/3ºimagenn.png" alt="1ºimagenn" style="zoom:80%;" />

| Settings                | Value                                                      |
| ----------------------- | ---------------------------------------------------------- |
| Subscription            | Nuestra Subscripcion                                       |
| Resource group          | **az104-10-rg1**                                           |
| Vault Name              | **az104-10-rsv1**                                          |
| Virtual network gateway | **None**                                                   |
| Region                  | **Region donde se desplegaran anterionmente las maquinas** |

Configuramos el backup

<img src="/img/5ºimagenn.png" alt="1ºimagenn" style="zoom:80%;" />

Dejamos la configuración en Geo-redundant

Configuramos la seguridad y confirmamos que este el Soft Delete habilidad

<img src="/img/6ºimagenn.png" alt="6ºimagenn" style="zoom:80%;" />

### TASK 3:

------

Configuramos el Backup en **Home->Recovery Service Vault >Overview> + Backup**

| Settings                        | Value                                                      |
| ------------------------------- | ---------------------------------------------------------- |
| Where is your workload running? | **Azure**                                                  |
| What do you want to backup?     | **Virtual machine**                                        |
| Vault Name                      | **az104-10-rsv1**                                          |
| Virtual network gateway         | **None**                                                   |
| Region                          | **Region donde se desplegaran anterionmente las maquinas** |

Confirmamos que ha sido creado el backup

<img src="/img/10ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

Generamos el backup



<img src="/img/11ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

### TASK 4:

------

Se implementaran las copias de seguridad mediante Azure recovery services

Nos conectamos a la maquina VM1 mediante RDP, iniciamos sesión en el portal vamos al recovery service vault y creamos un nuevo backup

**Home->Recovery Service Vault-> + Backup**

<img src="/img/13ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

Nos descargamos el  **Microsoft Azure Recovery Services Agent Setup Wizard** y procedemos al registro, esto iniciara **Register Server Wizard** registramos el backup generando una passphrase y almacenandola en documentos(Habitualmente no se guarda el pass en el sitio donde se realiza el backup)



<img src="/img/14ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

Configuramos el cronograma de backups, y tras esto podremos realizar el backup -> Backup Now

<img src="/img/16ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

<img src="/img/15ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

Seleccionamos ********C:\Windows\System32\drivers\etc\******** hosts , lo demas lo dejamos con valores por defecto, excepto el cronograma que lo podemos modificar al gusto

Comprobamos que el backup se crea dentro del portal:

<img src="/img/17ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />



### TASK 5:

------

Vamos a realizar la restauración mediante archivo:

Borramos el archivo de Hosts de la ruta **C:\Windows\System32\drivers\etc\** dentro de nuestra VM1

<img src="/img/18ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

Lo dejamos borrado y procedemos a recuperarlo dentro del Microsoft Azure Backup, seleccionamos nuestra maquina, el metodo mediante Archivos y carpetas individuales, indicamos el volumen y montamos, una vez montado hemos de hacer un robocopy:

<img src="/img/19ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

<img src="/img/20ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

***robocopy [recovery_volume]:\Windows\System32\drivers\etc C:\Windows\system32\drivers\etc hosts /r:1 /w:1***



Comprobamos que el archivo vuelve a encontrarse en su ubicacion

<img src="/img/21ºimagenn.png" alt="10ºimagenn" style="zoom:80%;" />

### TASK 6:

------



### TASK 7:

------

