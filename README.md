# RoutersConfig
| Nombre | Carnet | Grupo |
| -------|--------|-------|
|Pablo Josué Barahona Luncey| 202109715| 7 |

Se creó la siguiente topología con el fin de poder conectar todas las VPC's entre sí, utilizando routers y switches.

![WhatsApp Image 2023-09-18 at 5 04 37 PM](https://github.com/Barahona1602/RoutersConfig/assets/98893615/589a1556-46b0-4876-a65f-ada5e2dd1abf)

## Configuración routers
Estos son los comandos que se ingresaron para configurar cada router, acá se configura la conexión al switch, posteriormente la configuración de conexión a los 2 routers y por último el rout estático a los otros 2 routers
El rout estático se configura de la siguiente manera:

ip route <red_destino> <máscara_subred> <salto.>

Por ejemplo al comunicarnos de R1 a R2 utilizamos 
```sh
ip route 192.168.131.0 255.255.255.0 172.132.0.2
```

A continuación los comandos de configuración de los routers:
### R1

```sh
conf t
int f0/0
ip address 192.168.132.1 255.255.255.0
no shutdown
end
conf t
int s1/1
ip address 172.132.0.1 255.255.255.0
no shutdown
end
conf t
int s1/0
ip address 172.131.0.1 255.255.255.0
no shutdown
end
conf t
ip route 192.168.131.0 255.255.255.0 172.132.0.2
end
conf t
ip route 192.168.133.0 255.255.255.0 172.131.0.2
end
copy running-config startup-config
```
Y esta es su tabla de ruteo:

![image](https://github.com/Barahona1602/RoutersConfig/assets/98893615/3a18ece4-a5de-41aa-ab1f-55ec64426ce0)

### R2

```sh
conf t
int f0/0
ip address 192.168.133.1 255.255.255.0
no shutdown
end
conf t
int s2/0
ip address 172.131.0.2 255.255.255.0
no shutdown
end
conf t
int s2/1
ip address 172.133.0.1 255.255.255.0
no shutdown
end
conf t
ip route 192.168.132.0 255.255.255.0 172.131.0.1
end
conf t
ip route 192.168.131.0 255.255.255.0 172.133.0.2
end
copy running-config startup-config
```
Y esta es su tabla de ruteo:

![image](https://github.com/Barahona1602/RoutersConfig/assets/98893615/0a56b41b-adb0-4c2e-8541-b4278f77fad7)

### R3

```sh
conf t
int f0/0
ip address 192.168.131.1 255.255.255.0
no shutdown
end
conf t
int s3/0
ip address 172.132.0.2 255.255.255.0
no shutdown
end
conf t
int s3/1
ip address 172.133.0.2 255.255.255.0
no shutdown
end
conf t
ip route 192.168.132.0 255.255.255.0 172.132.0.1
end
conf t
ip route 192.168.133.0 255.255.255.0 172.133.0.1
end
copy running-config startup-config
```
Y esta es su tabla de ruteo:

![image](https://github.com/Barahona1602/RoutersConfig/assets/98893615/dde3f1dc-523b-4386-9a9c-91612bf28191)

## Ping entre hosts
### Ping entre PC1 (R1) a PC3 (R2) y a PC5 (R3)

![WhatsApp Image 2023-09-18 at 4 57 58 PM](https://github.com/Barahona1602/RoutersConfig/assets/98893615/ba641299-a22a-498e-8bf3-a8a58c734018)

### Ping entre PC3 (R1) a PC1 (R1) y a PC5 (R3)
![WhatsApp Image 2023-09-18 at 4 59 54 PM](https://github.com/Barahona1602/RoutersConfig/assets/98893615/51492cda-0739-4921-82b9-a8fa75768d95)

### Ping entre PC5 (R1) a PC3 (R2) y a PC1 (R1)
![WhatsApp Image 2023-09-18 at 5 01 29 PM](https://github.com/Barahona1602/RoutersConfig/assets/98893615/1d492c4e-17f6-4e60-9b9c-79d1b6227558)
