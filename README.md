# GIT - Sistema de vercionamento de arquivo

O Git é um software livre, inicialmente projetado e desenvolvido pelo engenheiro Linus Torvalds para o desenvolvimento do Kernel Linux. 

É um dos sistemas de controle de versões mais usados hoje, principalmente para desenvolvimento de softwares porque é um software **livre e de código aberto**, é **rápido e eficiente** e é **distribuído** ( cada desenvolvedor possui uma cópia completa do histórico do projeto em seu próprio computador, o que oferece grande flexibilidade e resiliência, já que você pode trabalhar offline e manter o acesso a todas as funcionalidades do controle de versão.)

**ESTRUTURA .GIT**

- pasta oculta (coração do git) que guarda todas as informações de versionamento do repositório, contendo o histórico de commits, branches, tags,configurações, etc
    - HEAD → Aponta para o commit/branch atual.
    - config → Arquivo de configurações do repositório
    - objects/ → Onde o Git guarda os objetos do histórico (commits, blobs, árvores)
    - refs/ → Referências para branches e tags
    - logs/ → Registros de ações feitas no repositório

### Ciclo de vida do arquivo no Git

**Untracked (não rastreado)**

- Arquivo novo que você criou na pasta, mas o Git **ainda não está acompanhando**.
- Se rodar `git status`, ele aparece em vermelho.

**Staged (ou Index / Área de Stage)**

- Quando você roda `git add *arquivo*`, o arquivo vai para a staging area.
- Significa que você preparou esse arquivo para o próximo commit. Agora o Git sabe que você quer salvar essa versão dele.
- No `git status`, aparece em verde.

**Committed (ou Versionado)**

- Depois que você roda `git commit -m '*mensagem'*`, o arquivo é salvo no histórico do repositório. Ou seja, virou parte oficial da linha do tempo do seu projeto. Agora você consegue voltar a essa versão no futuro se precisar.

**COMANDOS:**

`git status` mostra estado atual dos arquivos do repositório.

`git add *arquivo` ou* `git add .`  **adiciona as modificações em *staging*, onde decidimos quais mudanças incluir no commit

`git restore --staged *arquivo`* para tirar o arquivo da stage area, mantendo as modificações 

`git restore *arquivo`* para voltar ao arquivo anterior, antes das modificações (apaga as modificações)

`git reset -soft HEAD-1` para apagar o último commit

### Conceitos básicos

1. **REPOSITÓRIO** - diretório onde o projeto é armazenado, onde o Git rastreia todas as mudanças feitas no projeto. 
    
    **🏷️ | Criando repositório** 
    
    - No GitHub: Icone do perfil → Repositories → New
    
    **🏷️ | Conectando ao repositório local** 
    
    - `cd Desktop`  →  `cd git-github-pretalab` → `git remote add origin *URL do repositório` →*  `git branch -M main`
    
    **COMANDOS:**
    
    `git remote -v`  é usado para listar os repositórios remotos associados ao seu projeto Git, mostrando também as URLs usadas para buscar (fetch) e enviar (push) dados.
    
    `git init` inicia um novo repositório git na pasta local
    
2. **COMMIT** - salvar alterações no seu projeto 
    - `git commit -m '*mensagem'*`
    
3. **PUSH** - enviar alterações do projeto do repositório local para o repositório remoto
    - `git push origin -u *nome-da-branch`* para primeira vez que vai usar o push em um novo repositório
    - `git push origin main` ****ou ****`git push`  depois do primeiro envio
        
        OBS.: A primeira branch do projeto é a main. 
        
    
4. **PULL** - puxar as últimas atualizações do repositório remoto para o repositório local
    
    

1. **BRANCH** - Ramificação no seu projeto a partir da linha cronologica principal.
    
    A primeira branch do projeto é a main. 
    
    Podemos criar branches para adicionar novas funcionalidades ou fazer correções de bugs no projeto. O propósito final é que as branches paralelas se encontrem com a branch main.
    
    - **Comandos para branch local**
        - `git checkout -b *nome-da-branch*` / `git switch -c *nome-da-branch` →* criar uma nova branch
        - `git branch -D *nome-da-branch*` → forçar deleção da branch
        - `git branch -d *nome-da-branch*` → deletar de forma segura, só quando as alterações forem mescladas
        - `git checkout *nome-da-branch*` / `git switch *nome-da-branch` →* trocar de branch
        - `git branch` → verificar as branches do projeto

![Branchs]("C:\Users\CPD\Desktop\workspace\pretalab-ciclo14-git-github\images\BRANCHS.png")
