# wb22-puppet

> Pregunta 1 : Aprovisiona un nuevo servidor debian 10 con la configuración cloud init adecuada para que haga join al puppetmaster directo.
```
#cloud-config
package_update: true
package_upgrade: true
runcmd:
  - apt update && apt install -y net-tools
  - echo puppet-agent2 > /etc/hostname
  - echo $(curl -s ipinfo.io/ip) puppet-agent2 >> /etc/hosts
  - echo 65.21.182.4 puppet-master.local puppet-master puppet >> /etc/hosts
  - hostname -F /etc/hostname
  - apt update && apt install -y puppet
  - systemctl enable puppet && systemctl start puppet 
  - puppet config set server 'puppet-master.local' --section main
  - puppet agent -t
```

> Dirígete ahora al agente y borra el archivo hosts. Luego prueba de ejecutar el agente a ver que ocurre.
> 
> Pregunta 3 : Vaya parece ser que no sabe resolver el host. Por eso siempre vamos a usar DNS de verdad. Borra los 2 servidores actuales y vuelve a desplegar 2 nuevos (uno master y uno agente) que usen DNS reales o si te atreves, regenera los certificados. Finalmente repite la misma prueba y asegurate de que sigue funcionando.
