> [Home](../README.md)

## Versionamento

- Utilizamos o [Git](https://git-scm.com/);
- Configurando a identidade no _git_:
  - A primeira coisa que deve ser feita após instalar _Git_ é configurar o "nome de usuário" e "endereço de e-mail".
  - Isto é importante, porque cada _commit_ usará essas informações para identificar quem realizou o _commit_:
    - `$ git config --global user.name "Fulano de Tal"`
    - `$ git config --global user.email "fulanodetal@exemplo.br"`
    - Essa configuração, é necessária realizar somente uma vez, pois isso utilizamos a opção `--global`. Dessa forma, o _Git_ utilizará essas informações para qualquer projeto utilizando essa instalação do _git_;
    - Caso seja necessário substituir essas informações para algum projeto específico, podemos executado os mesmos comandos dentro do diretório dos projetos, mas sem colocar a opção `--global`, dessa forma, somente o projeto dentro do diretório, terá as informações alteradas.

## Geração de chaves _ssh_ para acesso aos repositórios remotos

- Ao acessar o site do repositório, como por exemplo o [GitHub](https://github.com/), encontramos informações de como realizar a configuração das chaves _ssh_:
  - O site acessado em setembro de 2024 foi https://docs.github.com/pt/authentication, e conseguimos encontrar informações sobre os comandos de checagem das chaves existentes, geração de novas chaves e soluções de problemas;
  - Alguns comandos:
    - Checar as chaves existentes: `ls -al ~/.ssh`;
    - Verifique na listagem de chaves se existe alguma chave _SSH_ pública:
      - Por padrão, os nomes de arquivos de chaves públicas com suporte para o _GitHub_ são um dos seguintes:
        - _id_rsa.pub_
        - _id_ecdsa.pub_
        - _id_ed25519.pub_
    - Gerar a chave _ssh_ usada no _GitHub_: `ssh-keygen -t ed25519 -C "your_email@example.com" `:
      - **Obs.:** Até conseguimos gerar uma chave _ssh_ em um arquivo customizado, através do comando citado abaixo, que pegamos do site também citado abaixo. Mas o problema é que utilizar essa chave no _GitHub_, a conexão não estava sendo autorizada, resolvendo apenas ao gerarmos a chave sem alterar o nome do arquivo;
      - Executar o comando abaixo no terminal do _GitBash_, para gerar um arquivo chamado "id_git-hub":
        - `ssh-keygen -t ed25519 -C "your_email@example.com" -f /c/Users/Windows_Username/.ssh/id_git-hub`;
        - Essa dica foi obtida no mês de setembro de 2024 no site https://cloud.google.com/compute/docs/connect/create-ssh-keys?hl=pt-br#windows-10-or-later,
  - **Obs.:** Ao realizar o clone de algum servidor remoto, quando for realizada a autenticação, será solicitado que seja incluída a chave pública do repositório no arquivo _"known_hosts"_, que fica no mesmo diretório das chaves _ssh_.

## Ferramentas
- _**GitBash:**_ Um terminal instalado junto da instalação do _git_, permitindo utilizar os comando do _git_ em comando utilizados no _linux_; 
- _**[GitKraken](https://www.gitkraken.com/):**_ _GUI (graphical user interface)_ para a utilização do _Git_;

## Servidores remotos
- Podemos criar os repositórios remoto no [GitHub](https://github.com/), [BitBucket](https://bitbucket.org/) ou qualquer outro repositório remoto;
  - Após criado o repositório remoto, podemos criar o repositório local (através do terminal) e associar o remoto a esse local que foi criado:
  ```
  echo "# teste" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main
  git remote add origin git@github.com:Paulo-E-F-Fernandes/configuracao-de-ambientes.git
  git push -u origin main
  ```
  - **OU**, nas situações em que o repositório local já existir, para fazer o _push_, devemos seguir os seguintes passos:
  ```
  git remote add origin git@github.com:Paulo-E-F-Fernandes/configuracao-de-ambientes.git
  git branch -M main
  git push -u origin main
  ```
- **Exemplos:**
  - Entrar no diretório do projeto e executar os comandos:
    - `git init` - Para iniciar o repositório git local;
	- `git remote add [NOME_REPOSITÓRIO_REMOTO] [URL_REPOSITÓRIO_REMOTO]`;
	  - `git remote add origin git@github.com:Paulo-E-F-Fernandes/configuracao-de-ambientes.git` para **SSH**;
	  - `git remote add origin https://github.com/Paulo-E-F-Fernandes/configuracao-de-ambientes.git` para **HTTPS**.
	- `git remote -v` - Para verificar os repositórios remotos adicionados;

## Alguns problemas
- Caso ocorrer algum problema parecido com o abaixo:
  ```
  $ git pull origin master
  ssh: connect to host bitbucket.org port 22: Network is unreachable
  fatal: Could not read from remote repository.

  Please make sure you have the correct access rights
  and the repository exists.
  ```
- Podemos resolver usando o seguinte:
  - Abrir um console do *Git Bash*;
  - Digitar `nano  ~/.ssh/config`;
  - E depois, para o **Bitbucket**:
    ```
    Host bitbucket.org
      Hostname altssh.bitbucket.org
      Port 443
    ```
  - Para o **GitHub**
	```
	Host github.com
	  Hostname ssh.github.com
	  Port 443
	```

## Comandos úteis
- _**git add:**_ Adicionar os arquivos no _index_ do _git_;
- _**git commit:**_ Grava as alterações no repositório:
- _**git status:**_ Para identificar a situação da árvore de do _git_;
- 

> [Home](../README.md)