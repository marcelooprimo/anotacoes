# LISTA DE COMANDOS VARIADOS

Comandos utilizados em algum  momento da vida que ainda são uteis (ou não), que (talvez) ainda funcionem  :smile:

---
## calculos no shell utilizando o bc
```bash
bc <<< "scale=3; sqrt(2)" --> Calcula a raiz quadrada de 2
bc <<< "scale=2; 2*3.2" --> Calcula 2X3,2
```
---
## download playlist youtube
```bash
youtube-dl -o "%(title)s.%(ext)s" --youtube-skip-dash-manifest --yes-playlist endereco
```
---
## comando para listar a versão do pacote em cache
```bash
apt-cache showpkg squidguard
```
---
## Unir vários documentos pdf 
**(debian based)**
```bash
pdftk *.pdf cat output arquivo.pdf
```
 
 **(fedora based)**
```bash
pdfunite ColoringBook-page_3.pdf ColoringBook-page_7.pdf NewColoringBook.pdf
```
---
## Separar arquivo pdf
**(debian based)**
```bash
pdftk arq.pdf cat 12-15 output arq_pages12-15.pdf
```

**(fedora based)**
```bash
pdfseparate ColoringBook.pdf ColoringBook-page_%d.pdf
```
---
## procura um arquivo pelo conteúdo desejado 
```bash
find /etc/ | xargs grep -s -a -i "192.168.133.14"
```
ou
```bash
find . -type f -print | xargs grep --color "texto"
find . -type f -print0 | xargs -0 grep --color "some string"
```
---
## Exibe 10 últimas notícias do site gizmodo
```bash
lynx -source https://gizmodo.uol.com.br | grep 'rel="bookmark"' | sed 's/<[/]a>/\n/g ; s/<[^>]*>//g ;s/&#8220;/"/g ; s/&#8221/"/g; s/^[ \t]*//'
```
---
## Criar arquivo criptografado
### Criptografa arquivo utilizando AES256
```bash
gpg --cipher-algo AES256 -c [arquivo]
```
---
### Cria arquivo 7z criptografado
```bash
7z a -p -mx7 -mhe -t7z [nome arquivo].7z [arquivos]
```
---
## GPG
### Criar chave gpg
```bash
gpg --gen-key  #preencher os dados solicitados e digitar senha
```
ou 
```bash
gpg2 --full-gen-key
```

### Exportar chave pública
```bash
gpg -a --export ID CHAVE > nome_do_arquivo.pub
```
ou
```bash
gpg --export [--armor | -a] ID Usuario > nome_chave-pubkey.asc
```
ou
```bash
ssh-keygen -y <- preferível
```

### Listar chave privada
```bash
gpg -K
```
ou
```bash
gpg --list-secret-keys
```

### Exportar chave privada
```bash
gpg --export-secret-keys [--armor | -a] ID Usuario > nome_chave-privkey.asc
```

---
## Criar chave ed25519 para ssh 

```bash
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "Nova chave ssh para os servers"
```
>-o: Save the private-key using the new OpenSSH format rather than the PEM format. Actually, this option is implied when you specify the key type as ed25519.

>-a: It’s the numbers of KDF (Key Derivation Function) rounds. Higher numbers result in slower passphrase verification, increasing the resistance to brute-force password cracking should the private-key be stolen.

>-t: Specifies the type of key to create, in our case the Ed25519.

>-f: Specify the filename of the generated key file. If you want it to be discovered automatically by the SSH agent, it must be stored in the default `.ssh` directory within your home directory.

>-C: An option to specify a comment. It’s purely informational and can be anything. But it’s usually filled with `<login>@<hostname>` who generated the key.

---
## Expressão regular data formato AAAA-MM-DD
```bash
grep -E '^([0-9]){4}-(0[1-9]|1[0,1,2])-(0[1-9]|[1,2][0-9]|3[0,1])$'
```

---
## Listar os pentes de memória instalados no dispositivo
```bash
sudo dmidecode --type memory
```
---
## Comando para verificar se um host está com mDNS aberto
```bash
dig @ENDERECO_IP -p 5353 ptr _services._dns-sd._udp.local
```
---
## Comando para verificar se um host está com DNS recursivo
```bash
dig +short test.openresolver.com TXT @ENDERECO_IP_DO_HOST
```
---
## Utilizar servidor ssh como proxy
```bash
ssh -D porta -q -C -N USUARIO@SERVIDOR_SSH
```

>- após utilizar o comando acima, ir nas configurações do navegador e configurar SOCKS 5 como:
`localhost + porta escolhida no comando_ssh`

---
## Ler o conteúdo de um certificado digital .pem
```bash
openssl x509 -in ARQUIVO.PEM -noout -text
```
ou
```bash
openssl x509 -inform PEM -in ARQUIVO.PEM -text
```
## Exibe apenas a linha com o CN
```bash
openssl x509 -in certificado.com.br.pem -noout -text | grep -i "subject:"
```

Resultado:
Subject: C = BR, ST = SP, L = Campinas, O = EMPRESA, CN = DOMINIO

---
## Comandos SQL diretamente do terminal
```bash
mysql -u <usuário> -p<senha> -D <banco> -e <Comando SQL (SELECT, UPDATE, INSERT, DELETE e etc)>
```


---
## Execução do ZAP via CLI (Quando não há a possibilidade de utilizar tela)
```bash
/opt/zaproxy/zap.sh -dir <diretório de trabalho> -cmd -quickurl <URL> -quickout <caminho para o arquivo .xml> -quickprogress
```

### Checagem no domínio https://www.site.com.br/ salvando o resultado do relatório em /home/usuario/testes_web/site.xml
```bash
/opt/zaproxy/zap.sh -dir /home/usuario -cmd -quickurl https://www.site.com.br/ -quickout /home/usuario/testes_web/site.xml -quickprogress
```
---
## ER IF
```bash
if [[ "$hosts" =~ ^192\.168\.20[0-3]\.(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[1-9][0-9]|[1-9])$ ||\
     "$hosts" =~ ^192\.168\.70\.(25[0-5]|2[0-4][0-9]|19[2-9])$ ||\
     "$hosts" =~ ^172\.8\.96\.(25[0-5]|2[0-4][0-9]|1[3-9][0-9]|12[8-9])$ ||\
     "$hosts" =~ ^172\.220\.1\.(25[0-5]|2[0-4][0-9]|1[3-9][0-9]|12[8-9])$ ]];

EX:
192\.168\.20[0-3]\.(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[1-9][0-9]|[1-9]) = 192.168.200-203.1-255
```
---
## Execução WPSCAN
 ```bash    
wpscan --disable-tls-checks --force --random-user-agent --url <URL>     
```
---
## Comparar 2 certificados com openssl
```bash
diff <(openssl x509 -inform PEM -in arquivo.pem -text -noout) <(openssl x509 -inform PEM -in arquivo2.pem -text -noout)
```
---
## Busca arquivos duplicados 
```bash
find . ! -empty -type f -exec md5sum {} + | sort | uniq -w32 -dD | tr -s ' '
```
---
## Reduz o tamanho de /var/log/journal para 1G
```bash
sudo journalctl --vacuum-size=1G
```
---
## Extrair tar.gz para um diretório específico
```bash
tar -zxvf arquivo.tar.gz -C /local/diretorio
```
---
## Download de arquivos utilizando o cURL
```bash
curl -o /local/destino -C - URL_do_arquivo
```
EX: 
```bash
curl -o /home/linux10complica/ebook.pdf -C – https://www.linuxvoice.com/issues/016/Linux-Voice-Issue-016.pdf
```
## Utilizando o cURL com um agente diferente
```bash
curl -H "User-agent: AGENTE" -s -v URL
```
EX: 
```bash
curl -H "User-agent: Mozilla/5.0 (X11; Linux i686; rv:80.0) Gecko/20100101 Firefox/80.0" -s -v https://www.security.unicamp.br/security.asc
```
## Utilizar o cURL para descobrir o IP público
```bash
curl ipinfo.io
```
ou
```bash
curl -s http://whatismyip.akamai.com
```
ou
```bash
curl -s https://4.ifcfg.me
```
ou
```bash
curl -s www.meuip.com.br | grep -Eoi "Meu ip é [0-9.]+"
```

## Previsão do tempo diretamente do shell
```bash
curl http://wttr.in/LOCALIDADE
```

EX: 
```bash
curl http://wttr.in/campinas-sp # Mostra a previsão do tempo para os dias seguintes
```
ou
```bash
curl http://v2.wttr.in/LOCALIDADE # Mostra a previsão mais um gráfico de precipitação
```

---
## Download arquivo com wget em um diretório específico
```bash
wget URL -P DIRETÓRIO
```
Ex: 
```bash
wget -c https://cdimage.debian.org/images/cloud/buster/20210329-591/debian-10-generic-amd64-20210329-591.qcow2 -P ~/Downloads
```
---
## Adicionar usuário a um grupo secundário
```bash
usermod -aG grupo usuário
```

Para mudar o grupo primário é:
```bash
usermod -g grupo usuário
```

---
## Gerar senha usando pwgen
 Abaixo temos um exemplo da criação de 20 senhas com 20 caracteres sem os caracteres ```"`^~```
```bash
pwgen -ncBsy -r '"`^~' 20 20
```
---
## Snipet utilizando inotify para monitorar a criação de um arquivo no /tmp

>inotifywait é fornecido por inotify-tools no ubuntu

```bash
inotifywait -m /tmp -e create -e moved_to |
    while read dir action file; do
        echo "The file '$file' appeared in directory '$dir' via '$action'"
        # do something with the file
    done
```
---
## Busca de usuário no ldap
```bash
ldapsearch -x -H ldaps://HOST -b "dc=DOMINIO,dc=br" -D"uid=USERNAME,ou=people,dc=DOMINIO,dc=br" -W uid=USERNAME_A_SER_PESQUISADO
```
---
## reduzir tamanho de pdf

**usando ghostscript**
```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```

**usando ps2pdf**
```bash
ps2pdf -dPDFSETTINGS=/ebook input.pdf ps2pdf.pdf
```
---
## Exibir somente o que contém em 2 arquivos
```bash
diff --new-line-format="" --unchanged-line-format=""  file1 file2 < LEMBRAR DE PESQUISAR MELHOR SOBRE
```
---
## Comandos vim
| Comando | Explicação |
| ---|--- |
| `:sp filename` | Open filename in horizontal split |
| `:vsp filename` | Open filename in vertical split |
| `Ctrl-w h` ou `Ctrl-w ←` | Shift focus to split on left of current |
| `Ctrl-w l` ou `Ctrl-w →` | Shift focus to split on right of current |
| `Ctrl-w j` ou `Ctrl-w ↓` | Shift focus to split below the current |
| `Ctrl-w k` ou `Ctrl-w ↑` | Shift focus to split above the current |
| `Ctrl-w n+` | Increase size of current split by n lines |
| `Ctrl-w n-` | Decrease size of current split by n lines |



---
## Converter HTML em docx ou em outro formato (precisa utilizar o filtro correto)
```bash
soffice --headless --infilter=writerglobal8_HTML --convert-to docx:'MS Word 2007 XML' --outdir <diretorio de destino> <caminho do arquivo html>
```

---
## Testar várias imagens docker com grype
```bash
for image in $(docker image ls | grep PALAVA-CHAVE | tr -s ' ' | cut -f1-2 -d' ' | tr ' ' ':'); do echo "$image"; grype "$image" | tee ~/"${image#PALAVRA CHAVE/}"; done
```

---
## Copiar ou colar item da área de transferência
* Copiar um item:
```bash
xclip -selection clipboard
```
* Colar um item:
```bash
xclip -selection clipboard -o
```
**Exemplos:**
* Copiar a saída de um script ou comando no terminal diretamente para a área de transferência:
```bash
ls -l | xclip -selection clipboard
```
* Enviar um conteúdo da área de transferência para um comando no terminal:
```bash
xclip -selection clipboard | jq
```