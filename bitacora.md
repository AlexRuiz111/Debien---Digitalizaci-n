# BITÁCORA

## 1.- Preparación de la máquina
- Se desplegó una máquina virtual mínima en Proxmox.
- Se ejecutó la actualización completa del sistema operativo y se instalaron herramientas las esenciales.
- Se otorgaron permisos de administración al usuario principal. La contraseña de "root" se dejó vacía.
- Tras ciertas configuraciones específicas y de red, la máquina virtual se convirtió en una plantilla.

## 2.- Clonación de la plantilla
- Se generaron dos clones completos de la plantilla: **dev.grupo2** como entorno de desarrollo y **pro.grupo2** como entorno de producción.

## 3.- Configuración de red
- Se configuró la interfaz de red principal (ens18) de ambas máquinas virtuales editando el archivo "/etc/network/interfaces" para asignar direccionamiento estático dentro de la subred del aula.

**Comando ejecutado:**
  ```bash
  sudo nano /etc/network/interfaces
  ```

**dev.grupo2:**
```plaintext
allow-hotplug ens18
iface ens18 inet static
    address 192.168.1.49/24
    gateway 192.168.1.1
```

**pro.grupo2:**
```plaintext
allow-hotplug ens18
iface ens18 inet static
    address 192.168.1.50/24
    gateway 192.168.1.1
```

## 4. Cambios y verificación
- Se aplicaron los cambios en la configuración de red ejecutando el comando:
  ```bash
  sudo systemctl restart networking
  ```
- Se realizaron pruebas mediante el comando `ping` entre ambas máquinas y se verificó una comunicación exitosa.

## 5. Copia de seguridad
- Se generó una snapshot inicial en ambas máquinas desde la interfaz web de Proxmox, nombrada "recien-clonada".
