# Comandos GIT Básico
---

Quando digo básico no início do doc é porque é básico mesmo :smile:

A proposta é colocar os comandos mais úteis para meu dia a dia, ou seja, se aprendi algo novo, vou colocar aqui também, obviamente esse arquivo talvez faça sentido apenas para mim, pois há muitos cheatsheet que atenderão de maneira mais satisfatória e completa. Todos os comandos são executados diretamente no diretório clone do repositório remoto.

---

## Git semântico (usado em commits)

De forma simples: 

A idéia é facilitar e informar no PR a proposta do código. Algumas opções são:

- **feat:** A new feature
- **fix:** A bug fix
- **docs:** Documentation only changes
- **style:** Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **refactor:** A code change that neither fixes a bug nor adds a feature
- **perf:** A code change that improves performance
- **test:** Adding missing or correcting existing tests
- **chore:** Changes to the build process or auxiliary tools and libraries such as documentation generation

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
ou
```bash
git push --set-upstream origin <NOME DA BRANCH>
```
>Se for fazer o push direto na branch master ou na branch main só digitar git push (e torcer para não dar ruim :rofl:)
---
## Alterna a branch
```bash
git checkout <NOME DA BRANCH>
```
---
## Remove uma branch
```bash
git branch -d <NOME DA BRANCH>
```
## Exibe o log dos commits
```bash
git log
```