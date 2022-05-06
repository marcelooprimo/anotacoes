# Comandos GIT Básico
---

Quando digo básico no início do doc é porque é básico mesmo :smile:

A proposta é colocar os comandos mais úteis para meu dia a dia, ou seja, se aprendi algo novo, vou colocar aqui também, obviamente esse arquivo talvez faça sentido apenas para mim, pois há muitos cheatsheet que atenderão de maneira mais satisfatória e completa.

---

## Clonar um repositório
```bash
git clone <LINK DO REPOSITORIO>
```
---
## Criar uma branch
```bash
git checkout -b <NOME DA BRANCH>
```
---
## Exibir status da branch
```bash
git status
```
---
## Adicionar arquivos para realizar o Pull Request
```bash
git add <ARQUIVO OU CAMINHO DO ARQUIVO>
```
Ex:
```bash
git add .
```
ou 
```bash
git add <DIRETORIO>/ARQUIVO
```
---
## Realizar o commit
```bash
git commit -m "<COMENTÁRIO>"
```
---
## Realizar um push
```bash
git push origin <NOME DA BRANCH>
```
[!INFO]
>Se for fazer o push direto na branch master ou na branch main só digitar git push (e torcer para não dar ruim :rofl:)
