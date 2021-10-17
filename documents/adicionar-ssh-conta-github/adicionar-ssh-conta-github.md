# Como adicionar SSH na conta do GitHub

OBS: Repositorios ja existente em sua maquina, quando for fazer ***git push***, avera erro.
Então tera que deletalo e fazer ***git clone*** novamente.

Digite:
```ssh-keygen -t rsa -b 4096 -C "seu_email@exemplo.com"```

Com isso você ira criar uma nova SSH em sua maquina.

Caso queira por uma senha, digite a em "Enter a file in which to save the key", caso contrario
pule dando ***enter*** em tudo.

Adicionando a chave ao ssh-agent:

```$ eval "$(ssh-agent -s)"```

Agora adicione a chave privada ssh no ssh-agent

```$ ssh-add ~/.ssh/id_rsa```

Copie a ssh e cole no gitHub

```$ cat ~/.ssh/id_rsa.pub```

Teste a conexao da ssh.

```ssh -T git@github.com```
