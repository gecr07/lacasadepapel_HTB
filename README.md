# lacasadepapel HTB

# NMAP 

![image](https://github.com/gecr07/lacasadepapel_HTB/assets/63270579/7c21337c-8e5b-4da0-9885-e4673da0b875)


## RCE

Se explota la version de ftp "vsftpd 2.3.4. Este exploit si lo revisas abre una shell en el puerto 6200. 


![image](https://github.com/gecr07/lacasadepapel_HTB/assets/63270579/b8eb9739-6b88-4418-b318-def922cabdbc)

Se mete nuestra public key en authorized keys pero al entrar nos manda otra vez a la Psy Shell. Para aprobechar esto vamos a usar el Dinamic port fowarding


```
ssh -i id_rsa dali@10.129.242.42 -D 1080
# Puerto configurado tambien el proxychains si acepta sock5
```

Para verificar que si tenemos acceso a los puertos de la maquina utiliza

```
proxychains nmap -p 1-10000 $target
```

Para iniciar el firefox con proxychains tienes que ver el output parecido a este:

![image](https://github.com/gecr07/lacasadepapel_HTB/assets/63270579/a3fd1aec-53e8-42b8-9ec4-88a1e3fe9913)


### LFI 

Nos encontramos un LFI





































