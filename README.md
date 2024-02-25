# RHCE-LABS-VAGRANT

Vagrantfile creado para un laboratorio de RHCE utilizando la imagen de Redhat Enterprise Linux 9.3

Se crean 3 maquinas virtuales:
- control.example.local
- ansible1.example.local
- ansible2.example.local

Cada maquina virtual tiene las siguientes caracteristicas:

- 1 NIC NAT
- 1 NIC intnet
- 1 disco storage (sistema)
- 1 disco extra (sin formato)

La NIC intnet se va a configurar con el rango de red "192.168.29.0/24" en caso se requiera modificar la direccion IP debes modificar el rango en el Vagrantfile.