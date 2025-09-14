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
    
    

5. **BRANCH** - Ramificação no seu projeto a partir da linha cronologica principal.
    
    A primeira branch do projeto é a main. 
    
    Podemos criar branches para adicionar novas funcionalidades ou fazer correções de bugs no projeto. O propósito final é que as branches paralelas se encontrem com a branch main.
    
    - **Comandos para branch local**
        - `git checkout -b *nome-da-branch*` / `git switch -c *nome-da-branch` →* criar uma nova branch
        - `git branch -D *nome-da-branch*` → forçar deleção da branch
        - `git branch -d *nome-da-branch*` → deletar de forma segura, só quando as alterações forem mescladas
        - `git checkout *nome-da-branch*` / `git switch *nome-da-branch` →* trocar de branch
        - `git branch` → verificar as branches do projeto

![Branchs]("C:\Users\CPD\Desktop\workspace\pretalab-ciclo14-git-github\images\BRANCHS.png")


6. **MERGE** - mesclagem de branches
    
    🏷️ | união das branches (com MERGE)
    
    - na branch **main** : faz a modificação → salva (ctrl + s) → `git add *arquivo`* → `git commit -m "*mensagem*"` → `git push`
    - na branch **feature :** `git merge`
    
7. **REBASE** - similar ao merge, reorganiza o histórico de commits apagando ou combinando-os para um histórico mais limpo (linear). É recomendado para a integração de mudanças entre branches de desenvolvedores, antes do envio ao branch principal.  É usado antes de dar push, pull request e outros comandos, pois aAplica os commits da branch atual e os coloca “no topo” da branch base 
    
    
    **COMANDOS:** 
    
    na branch **feature** : `git rebase main` →  `git push` 
    
    - caso haja conflitos: resolve o conflito utilizando o `merge` → `git add *arquivo`* → `git commit -m "*mensagem*"` → `git rebase --continue` → repete até que todos os conflitos sejam resolvidos → `git push --force`
    
    `git rebase --continue` para continuar depois de resolver conflitos
    
    `git push --force` para forçar o push, já que a versão é diferente da que está no arquivo remoto. 
    
    - ⚠️ **ATENÇÃO:**  esse comando pode apagar versões e commits em trabalhos colaborativos.
    
8. **FORK** - criar uma cópia de um projeto preexistente no seu GitHub sem mudar o repositório original.
    
    **Como fazer um Fork no GitHub:** 
    
    - Vá até o repositório original no GitHub → Clique no botão **Fork** (fica no canto superior direito). → Escolha sua conta ou organização para criar a cópia
    - Agora, no seu repositório (forkado), clique em **Code** → copie a URL (pode ser HTTPS ou SSH).
    
9. **CLONE** - criar uma cópia total do repositório remoto no computador local, lhe permitindo trabalhar no projeto de maneira independente. 
    
    Pode usar o repositório, mas para subir alterações, precisa de permissão.
    
    `git clone *URL-do-reposorio-forkado*`
    
    **➕ EXTRA ➕**
    
     Quando você forka um repositório remotamente e clona na suamáquina,  as atualizações do projeto original não puxadas com o gitpull.  Caso queira puxar as atualizações da branch main (do projeto original) para a sua main, é necessário seguir os comandos abaixo: 
    
    Na branch main, “conecte” o seu repositório local com o repositório remoto original: `git remote add upstream *URL-do-repositório*`
    
    Puxe as mudança do repositório original: `git fetch upstream`
    
    Atualiza a branch main local de vocês: `git merge upstream/main`
    
    Envia as mudanças para o fork de vocês: `git push origin -u main` / `git push`
    
10. **PULL REQUEST** - Solicitar que as mudanças (branchs/forks) integram o projeto principal.
    
    **Boas práticas de Pull Request:**
    
    - **Titulo:**
        - Seja claro e objetivo → O título deve resumir a mudança feita.
        - Use verbos no imperativo (mesma ideia dos commits) → facilita entender a ação.
        - Mantenha consistente com o padrão do time → alguns usam prefixos como: feat para novas funcionalidades, fix para correções, docs para mudanças na documentação, refactor para refatorações
    - **Descrição:**
        - Contexto: explique o porquê da mudanças
        - O que foi feito: detalhe as alterações principais.
        - Como testar: se aplicável, explique como alguém pode validar a mudança.
        - Screenshots / exemplos: se for visual (como gráficos ou interfaces), inclua imagens.
        - Checklist (opcional): ajuda a organizar o que foi feito.

### Comandos básicos de Git

`git init` - inicia um novo repositório git na pasta local

`git add *arquivo` ou* `git add .` *-* adiciona as modificações em *staging*, onde decidimos quais mudanças incluir no commit

`git status` - estado atual dos arquivos do rep. 

`git commit -m '*mensagem'` -* cria um commit salvando as mudanças no histórico com uma mensagem

`git pull` - atualiza o rep. local com as mudanças mais recentes do rep. remoto.

`git push` - atualiza o rep. remoto com as mudanças mais recentes do rep. local

`git remote add origin *URL do repositório*` -  conecta seu rep. local a um remoto no GitHub

`git checkout '*arquivo'*` - desfaz alterações locais em um arquivo específico revertendo-o para a última versão confirmada (commited)

`git log` / `git log --oneline` - histórico de commits

`git diff` / `git diff hash01 hash02` - diferenças entre versões

### Configuração inicial

`git config --global user.name "*nome-de-usuário*"` - define o nome de usuário associado aos seus commits

`git config --global user.email "*email@exemplo.com*"` - define o email associado aos seus commits

`git config --list` - mostra todas as configurações ativas naquele ambiente

- `core.autocrlf=true` → configuração de quebra de linha.
- `credential.helper=manager` → como o Git salva credenciais.
- `init.defaultbranch=master` → nome padrão do primeiro branch.
- `user.name` e `user.email` → suas infos.

## GITHUB

O GitHub é a plataforma remota onde guardamos os arquivos do GIT. 

### CHAVE SSH

É um par de chaves (pública + privada) que você gera no seu computador para autenticar de forma segura sua máquina com o repositório remoto. Isso cria uma "identidade digital" que permite se conectar sem precisar digitar usuário/senha sempre.

- A chave privada fica só com o usuário, enquanto a pública é cadastrada no GitHub.

### 🏷️ |  Chave de segurança

`ls ~/.ssh` - verificação da chave de segurança

- Caso não tenha, utilizar pra criar: `ssh-keygen -t ed25519 -C "seu-email@exemplo.com"`

### 🏷️ |  Ativação da chave

`eval "$(ssh-agent -s)”`→ `ssh-add ~/.ssh/id_ed25519`

### 🏷️ |  Adicionar chave no GitHub

`cat ~/.ssh/id_ed25519.pub`→ copia a chave completa 

- **No GitHub:** Icone do perfil → Settings → SSH and GPG keys → New SSH key → Colar a a chave e adicionar um titulo (security_pub-key) → Salvar chave

### 🏷️ |  Verificação da chave SSH

`ssh -T git@github.com`

### Ferramentas e boas práticas

**stach:** 

`git stash` guarda o arquivo temporariamente.

`git stash pop` retorna o arquivo guardado em ordem.

***.gitignore:***  

arquivo que guarda arquivos que não precisam ir para o repositório remoto.

**tags:** 

servem para marcar pontos específicos na linha do tempo do seu repositório. usadas para marcar lançamentos de software, versões estáveis ou pontos significativos no histórico do projeto.

`git tag *v1.0`* é apenas um marcador de commit sem não tem autor, mensagem, data.

`git tag -a *v1.0* -m "*mensagem*"`  versão mais completa que guarda autor, mensagem e data. 

`git tag --list` lista de tags do projeto.

`git push origin *versão`* envia as tags (o push por si só não envia as tags).

`git tag -d v1.0.0` para apagar tags locais.

`git push origin --delete tag v1.0.0` para apagar tags remotas. 

`git show v1.0.0` para mostrar detalhes da tag.

**alias:** 

atalhos personalizados para comandos do Git

`git config global alias.*apelido comando-que-quer-apelidar`* para apelidar o comando. 

`git *apelido`* para utilizar o comando

**outros:**

`git branch -vv` para verificar se a sua branch ta sendo rastreada no repositório remoto.

`git checkout -d *branch-a-ser-deletada`* para deletar a branch (é necessário estar em outra branch que não a que a gente quer deletar). 

`git checkout -D *branch-a-ser-deletada`* para deletar a branch de maneira FORÇADA no repositório local. 

`git push origin --delete *branch-a-ser-deletada`* para deletar a branch no repositório remoto. 

`git revert *id-do-commit`* para apagar o commit.