# Magalu – Crédito no Checkout (MagaluPay) · Arquitetura Corporativa (TOGAF + ArchiMate)

Repositório: **<https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura>**

Este guia explica como o grupo trabalha **no mesmo modelo ArchiMate**, cada aluno na **sua branch**, e como
**juntamos tudo no final sem perder nada** (elementos, relações, views, documentação, propriedades).

Ferramentas: **Archi 5.x** + plugin **coArchi** (Collaboration, testado com 0.9.7) + **Git/GitHub**.

> 📌 **Leia na ordem.** Seções 2 a 4 são feitas uma vez só. A seção 5 é o dia a dia. A 6 e a 7 são a hora de juntar.

---

## Sumário

1. [Por que coArchi e não o arquivo `.archimate` no Git](#1-por-que-coarchi-e-não-o-arquivo-archimate-no-git)
2. [Pré-requisitos e credenciais (token do GitHub)](#2-pré-requisitos-e-credenciais)
3. [Configuração inicial do repositório (já feita)](#3-configuração-inicial-do-repositório-já-feita)
4. [Configuração de cada aluno](#4-configuração-de-cada-aluno)
5. [Branches e ciclo de trabalho](#5-branches-e-ciclo-de-trabalho)
6. [Juntando tudo na `main`](#6-juntando-tudo-na-main-integração)
7. [Conflitos: como resolver sem perder nada](#7-conflitos-como-resolver-sem-perder-nada)
8. [Regras de ouro](#8-regras-de-ouro)
9. [Divisão do trabalho por fase do TOGAF](#9-divisão-do-trabalho-fases-do-togaf-adm)
10. [Arquivos extras no repositório (README, `.gitignore`)](#10-arquivos-extras-no-repositório-readme-gitignore)
11. [Checklist antes do Pull Request](#11-checklist-antes-de-abrir-o-pull-request)
12. [Problemas comuns](#12-problemas-comuns)

---

## 1. Por que coArchi e não o arquivo `.archimate` no Git

O arquivo `.archimate` é **um único XML gigante**. Se dois alunos alteram esse arquivo em branches diferentes,
o Git compara linha a linha e o merge quase sempre dá conflito ou, pior, **corrompe o modelo** (IDs duplicados,
relações apontando para elementos que não existem, views quebradas).

O coArchi salva o modelo no repositório **um arquivo por objeto**:

```
magalu-arquitetura/
├── README.md          ← este guia (o coArchi ignora)
├── .gitignore         ← proteção contra lixo (seção 10)
├── model/             ← O MODELO. Gerado pelo coArchi. Nunca edite à mão.
│   ├── folder.xml
│   ├── strategy/      ← ValueStream_id-xxxx.xml, Capability_id-xxxx.xml ...
│   ├── business/
│   ├── application/
│   ├── technology/
│   ├── motivation/    ← Stakeholder, Driver, Goal, Principle ...
│   ├── implementation_migration/
│   ├── other/
│   ├── relations/     ← cada relação é um arquivo
│   └── diagrams/      ← cada view é um arquivo ("0 - preliminar", "A - Vision", ...)
└── images/            ← imagens usadas nas views (gerado pelo coArchi)
```

Se o Aluno 1 cria elementos de Negócio e o Aluno 2 cria elementos de Tecnologia, **não existe conflito** — são
arquivos diferentes. Conflito só acontece quando duas pessoas editam **o mesmo objeto** (o mesmo elemento ou a
mesma view).

> ⚠️ **Ninguém edita mais o `.archimate` antigo.** Daqui em diante o trabalho é **somente** no modelo do
> coArchi. O `.archimate` vira apenas backup/entrega (exportado com *File ▸ Save As…*).

---

## 2. Pré-requisitos e credenciais

### 2.1 Programas

1. **Archi 5.x** — <https://www.archimatetool.com/download/>
2. **Plugin coArchi** — *Help ▸ Manage Plug-ins…* (ou baixe em <https://www.archimatetool.com/plugins/>).
   **Todos com a mesma versão** de Archi e de coArchi.
3. Conta no **GitHub** e ser adicionado como **colaborador** do repositório (peça ao Henrique — seção 3).

### 2.2 Criar o token do GitHub (obrigatório)

O GitHub **não aceita a senha da conta** para Git. Se você usar a senha, o Archi mostra:
`TransportException: ... not authorized`. Use um **Personal Access Token**:

1. GitHub ▸ sua foto (canto superior direito) ▸ **Settings** ▸ **Developer settings** (último item à esquerda)
   ▸ **Personal access tokens** ▸ **Tokens (classic)**.
2. **Generate new token ▾ ▸ Generate new token (classic)** (pode pedir senha/2FA).
3. **Note**: `Archi coArchi - magalu`.
4. **Expiration**: até o fim do semestre (ex.: *90 days* ou *Custom*). Evite *No expiration*.
5. **Select scopes**: marque **`repo`** (só isso).
6. **Generate token** e **copie na hora** (começa com `ghp_…`; o GitHub **não mostra de novo**).
   Guarde num gerenciador de senhas. **Nunca** cole o token em chat, README ou commit.

> Prefere *Fine-grained token*? Em **Repository access** escolha `magalu-arquitetura` e em
> **Repository permissions ▸ Contents** coloque **Read and write** (o padrão é só leitura e dá *not authorized*).

**Testar o token** (opcional, no terminal Linux/macOS — o token não aparece na tela):

```bash
read -rs "T?Token: "; echo; curl -s -H "Authorization: Bearer $T" \
  https://api.github.com/repos/Henrique-Melo-Rodrigues/magalu-arquitetura | grep -A6 '"permissions"'; unset T
```

(no **bash**, troque `read -rs "T?Token: "` por `read -rsp "Token: " T`). Precisa aparecer `"push": true`.

### 2.3 A janela "Primary Password" (não é a senha do GitHub!)

Na primeira vez que o coArchi for salvar a credencial, ele abre **Primary Password**. É uma senha **local,
inventada por você**, que só criptografa as credenciais guardadas no seu computador.

- **Current Primary Password**: deixe **em branco**.
- Opção **Set new primary password and generate new encryption key**.
- **New** e **Retype**: a senha que você quiser (anote). **OK**.
- Esqueceu? Basta criar outra — só terá que redigitar o token.

### 2.4 Usuário e e-mail

*Edit ▸ Preferences ▸ Collaboration ▸ General*: preencha **Nome** e **E-mail**. Eles aparecem nos commits —
é assim que o grupo e o professor veem quem fez o quê.

### 2.5 Linux com Wayland (Hyprland, Sway, GNOME…) ou tema GTK customizado

Sintoma: na janela *Primary Password* (ou de login) **as caixas de texto não aparecem / não dá para digitar**.
Solução: abrir o Archi via X11 e com o tema GTK padrão:

```bash
GDK_BACKEND=x11 GTK_THEME=Adwaita /opt/archi/Archi
```

Para deixar fixo, crie `~/.local/share/applications/archi.desktop` (cópia do atalho do sistema) com:
`Exec=env GDK_BACKEND=x11 GTK_THEME=Adwaita /opt/archi/Archi`.
Se ainda assim falhar, mude *Preferences ▸ Appearance ▸ Theme* para **Light** e reinicie.

---

## 3. Configuração inicial do repositório (já feita)

✅ Feito pelo Henrique — **não repita**. Fica registrado para referência:

1. Repositório **vazio** criado no GitHub (`magalu-arquitetura`).
2. No Archi: modelo aberto ▸ **Collaboration ▸ Add Local Model to Workspace and Publish** com a URL
   `https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura.git` (commit "First Commit").
3. Pendências do responsável:
   - [ ] Adicionar cada aluno em **Settings ▸ Collaborators** (sem isso o token dele dá *not authorized*).
   - [ ] Adicionar `README.md` e `.gitignore` pelo site (seção 10).
   - [ ] Proteger a `main`: **Settings ▸ Branches ▸ Add rule** ▸ `main` ▸ **Require a pull request before merging**.
   - [ ] Guardar o `.archimate` original como backup.

---

## 4. Configuração de cada aluno

1. Aceite o convite de colaborador (chega por e-mail / notificações do GitHub).
2. Crie seu token (seção 2.2).
3. No Archi: **Collaboration ▸ Import Remote Model to Workspace**.
   - URL: `https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura.git`
   - Usuário: **seu** login do GitHub · Senha: **seu token** · marque para salvar.
   - Defina a *Primary Password* (seção 2.3).
4. O modelo aparece na árvore de Modelos. **É nele que você trabalha.**
5. Abra as views auxiliares: **Window ▸ Collaboration Workspace**, **Branches** e **Change History**.

---

## 5. Branches e ciclo de trabalho

### 5.1 Nomes das branches

```
main                       ← versão oficial, integrada e revisada
aluno/<nome>-<fase>        ← trabalho de cada aluno
   ex.: aluno/henrique-faseB
        aluno/maria-faseC
        aluno/joao-faseD
```

Use letras minúsculas, sem acento e sem espaço.

### 5.2 Criar sua branch (no Archi)

1. **Refresh Model** (garante que você parte da `main` mais recente).
2. View **Branches** ▸ com `main` como branch atual ▸ **Add New Branch to Current Branch** ▸
   `aluno/<nome>-<fase>`.
3. Selecione a branch nova ▸ **Switch Branch** (o modelo na tela passa a ser o da sua branch).
4. **Publish Changes** para a branch existir no GitHub (backup + visibilidade para o grupo).

> Antes de trocar de branch, **sempre** faça *Commit Changes* do que estiver pendente.

### 5.3 Ciclo diário

```
Refresh Model → modelar → Save (Ctrl+S) → Commit Changes (mensagem clara) → Publish Changes
```

| Ação | O que faz | Quem vê |
|------|-----------|---------|
| **Save** | grava localmente | só você |
| **Commit Changes** | registra no histórico local | só você |
| **Publish Changes** | busca o remoto, junta e envia ao GitHub (*pull + push*) | todo o grupo |
| **Refresh Model** | traz o que os outros publicaram na **sua branch atual** | — |

- Sem **Publish**, ninguém vê seu trabalho e **não há backup**. Publique **ao fim de toda sessão**.
- Commits **pequenos e frequentes** (a cada view ou conjunto de elementos).
- Errou? **Abort Uncommitted Changes** descarta o que não foi commitado; **Undo the latest commit** desfaz o
  último commit (só se ainda não publicou).

### 5.4 Mensagens de commit

```
[Fase B] Cria view "Processos de Negócio do Checkout"
[Fase B] Adiciona atores Cliente, Lojista e Analista de Crédito
[Fase C] Relaciona App Magalu ao serviço de Análise de Crédito
[Ajuste] Corrige nome do Goal "Aumentar conversão no checkout"
```

### 5.5 Trazer a `main` para a sua branch (pelo menos 1x por semana)

Quanto mais tempo a branch fica isolada, maior e mais difícil o merge final.

1. *Commit Changes* de tudo que está pendente.
2. **Refresh Model** (atualiza as referências do GitHub, incluindo a `main`).
3. View **Branches** ▸ estando na **sua** branch, selecione `main` ▸ **Merge Branch into Current Branch**.
4. Se houver conflito, resolva (seção 7), abra as views afetadas e confira.
5. **Publish Changes**.

---

## 6. Juntando tudo na `main` (integração)

Fluxo: **Pull Request no GitHub** para revisar + **merge pelo Archi** quando houver conflito.

### 6.1 O aluno, ao terminar sua parte

1. Traga a `main` para sua branch (seção 5.5) — assim **você** resolve os conflitos da sua parte.
2. **Tools ▸ Validate Model** e corrija erros/avisos relevantes.
3. *Commit Changes* + *Publish Changes*.
4. GitHub ▸ **Pull requests ▸ New pull request** ▸ `base: main` ← `compare: aluno/<nome>-<fase>`.
   - Descrição: views criadas/alteradas, elementos compartilhados que você mexeu, o que falta.
   - Peça revisão de pelo menos **1 colega**.
5. Como cada objeto é um arquivo, a aba **Files changed** mostra exatamente o que entrou, saiu ou mudou.

### 6.2 O integrador (Henrique)

1. **Antes de cada merge**: com a `main` aberta no Archi, **File ▸ Save As…** →
   `backup-AAAA-MM-DD.archimate` **fora** da pasta do repositório. É o seu "desfazer".
2. PR **sem conflitos** → **Merge pull request** → *Create a merge commit*
   (**não** use *Squash*, para manter a autoria de cada aluno).
3. PR **com conflitos** → **não** resolva no editor web do GitHub (XML editado à mão quebra o modelo).
   Peça ao aluno para refazer a seção 5.5, ou faça no Archi: *Switch Branch* para `main` ▸ selecione a branch
   do aluno ▸ **Merge Branch into Current Branch** ▸ resolva ▸ *Publish Changes*.
4. **Um PR por vez**. Depois de cada um: *Refresh Model* ▸ *Validate Model* ▸ abrir as views da fase ▸ só
   então o próximo.
5. Ao fechar uma entrega, crie uma **tag/Release** no GitHub (**Releases ▸ Draft a new release ▸** tag
   `entrega-fase-B`) e anexe o `.archimate` exportado e o relatório HTML (*File ▸ Report ▸ HTML…*).

### 6.3 Todos, depois de um merge na `main`

Quem estiver na `main`: **Refresh Model**. Quem estiver em branch própria: seção 5.5.

---

## 7. Conflitos: como resolver sem perder nada

Conflito = **o mesmo objeto** alterado nas duas branches. O coArchi abre uma janela listando os objetos em
conflito e, **para cada um**, você escolhe **a minha versão (Ours)** ou **a do outro (Theirs)**.
Não existe "mesclar campo a campo" — por isso:

1. **Antes de escolher**, veja a diferença: abra a outra branch no GitHub e o arquivo do objeto
   (nome, *documentation*, *properties*, posição na view).
2. Escolha a versão **mais completa**.
3. Depois do merge, **reaplique à mão** o que a versão descartada tinha de diferente.
4. *Validate Model*, confira as views e faça o commit:
   `[Merge] Integra faseB; mantém documentação de X e posição de Y`.

> Em dúvida, **cancele o merge**, faça backup (*Save As…*) e chame o colega do outro lado do conflito.

Recuperar algo antigo: **Show Change History** ▸ selecione o commit ▸ veja o modelo daquele momento,
**Restore to this commit** ou extraia o modelo daquele commit.

**Nunca:**
- resolver conflito editando XML à mão (GitHub web, VS Code…);
- `git push --force` na `main` ou na branch de um colega;
- apagar a branch do aluno antes de confirmar que tudo dela está na `main`.

---

## 8. Regras de ouro

1. **Cada aluno é dono das suas views.** Não edite a view de outro sem combinar — views são o que mais gera
   conflito (posição, tamanho, cor, bendpoints).
2. **Elementos compartilhados são criados uma vez, na `main`** (ex.: `Cliente`, `Magalu`, `MagaluPay`,
   `App Magalu`, stakeholders e goals da Fase A). Antes de criar, **pesquise na árvore** do modelo; se já
   existe, **arraste o existente** para a sua view. Dois "Cliente" criados em branches diferentes **não geram
   conflito no Git**, mas geram **duplicata** (IDs diferentes) — erro difícil de achar depois.
3. **Não apague nem renomeie elementos que outros usam** sem avisar. Apagar remove o elemento e suas relações
   de **todas** as views. Veja onde é usado em *Properties ▸ Analysis (Model Relations)* antes.
4. **Não reorganize as pastas do modelo** sem combinar.
5. **Commit + Publish ao fim de cada sessão.**
6. **Refresh antes de começar**; traga a `main` toda semana.
7. **Mesma versão de Archi/coArchi para todos.**
8. **Documente no próprio modelo**: campo *Documentation* de elementos e views, e *Properties* quando útil
   (`autor`, `fase-ADM`, `status`). Assim nada "adicional" se perde — está versionado junto.
9. **Não coloque arquivos na pasta do repositório local** (`~/Documents/Archi/model-repository/…`).
   O coArchi faz commit de **tudo** que estiver lá (veja seção 10).

---

## 9. Divisão do trabalho (fases do TOGAF ADM)

| Pasta de Views                     | Situação                                          | Branch sugerida         |
|------------------------------------|---------------------------------------------------|-------------------------|
| `0 - preliminar`                   | Princípios de Arquitetura, Equipe de Arquitetura  | `main` (feito)          |
| `A - Vision`                       | Stakeholders/Drivers/Objetivos, Realização de Objetivos, Capacidades e Cadeia de Valor, Declaração de Trabalho | `main` (feito) |
| `B - Business`                     | vazia                                             | `aluno/<nome>-faseB`    |
| `C - Information Systems`          | vazia                                             | `aluno/<nome>-faseC`    |
| `D - Technology`                   | vazia                                             | `aluno/<nome>-faseD`    |
| `E - Opportunities and Solutions`  | vazia                                             | `aluno/<nome>-faseE`    |
| `F - Migration Planning`           | vazia                                             | `aluno/<nome>-faseF`    |

Dependências: **B → C → D → E → F**. Integre a Fase B cedo para que C e D reutilizem os elementos de negócio
(regra de ouro nº 2). C e D podem andar em paralelo.

| Aluno | Fase / views | Branch | Status |
|-------|--------------|--------|--------|
|       |              |        |        |
|       |              |        |        |
|       |              |        |        |

---

## 10. Arquivos extras no repositório (README, `.gitignore`)

### Como o coArchi trata arquivos fora de `model/` e `images/`

Verificado no código-fonte do coArchi
([`GraficoModelExporter`](https://github.com/archimatetool/archi-modelrepository-plugin/blob/master/org.archicontribs.modelrepository/src/org/archicontribs/modelrepository/grafico/GraficoModelExporter.java),
[`ArchiRepository`](https://github.com/archimatetool/archi-modelrepository-plugin/blob/master/org.archicontribs.modelrepository/src/org/archicontribs/modelrepository/grafico/ArchiRepository.java)):

- Ao salvar/commitar, o coArchi **apaga e recria apenas** `model/` e `images/`. Arquivos na raiz
  (`README.md`, `.gitignore`) **não são tocados** e **não interferem** no modelo.
- O commit do coArchi equivale a `git add .` — **tudo** que estiver na pasta do repositório local entra no
  commit, inclusive lixo (backups `.archimate`, relatórios, PDFs). Ele respeita o `.gitignore`.
- Por padrão ele ignora só `*.bak` e `.DS_Store`, e isso fica em `.git/info/exclude`, que **não é
  compartilhado**. Daí a utilidade de um `.gitignore` versionado.

### Forma segura de adicionar/editar o README e o `.gitignore`

Sempre **pelo site do GitHub**, direto na `main`:

1. Repositório ▸ **Add file ▸ Upload files** (ou **Create new file** e cole o conteúdo).
2. Commit direto na `main`, mensagem `docs: adiciona README e .gitignore`.
3. Todos fazem **Refresh Model** (quem está em branch própria: seção 5.5). O arquivo entra sem conflito,
   pois o modelo não mexe nele.

Regras:
- **Uma pessoa** edita o README por vez (é texto comum; dois editando a mesma linha dá conflito de Git normal).
- **Nunca** use o editor web para mexer em nada dentro de `model/` ou `images/`.

### O `.gitignore` recomendado (e o que **jamais** ignorar)

```gitignore
# ⚠️ NUNCA ignore model/, images/, *.xml ou *.png:
#    o coArchi deixaria de commitar o modelo SEM AVISAR.

# Cópias do modelo (o modelo oficial é a pasta model/)
*.archimate
*.archimate.bak
*.bak

# Relatórios/exportações (anexe em Releases, não no repositório)
/report/
/html-report/
/export/

# Sistema operacional / editores
.DS_Store
Thumbs.db
desktop.ini
*~
*.swp
.idea/
.vscode/
```

Por que ignorar `*.archimate`? Para ninguém commitar uma cópia do modelo que depois alguém edita
"por engano" achando que é a oficial. Os `.archimate` de entrega vão como anexo em **Releases** (seção 6.2).

---

## 11. Checklist antes de abrir o Pull Request

- [ ] *Refresh Model* e `main` trazida para minha branch (seção 5.5), sem conflitos pendentes
- [ ] *Validate Model* sem erros
- [ ] Não criei elementos duplicados de algo que já existia na `main`
- [ ] Não editei views de outros alunos
- [ ] Elementos e views novos têm *Documentation* preenchida
- [ ] Minhas views estão na pasta da fase correta
- [ ] *Commit Changes* + *Publish Changes* feitos; descrição do PR lista o que mudou

---

## 12. Problemas comuns

| Problema | Causa provável | Solução |
|----------|----------------|---------|
| `TransportException ... not authorized` | Senha da conta no lugar do token; token sem escopo `repo`; não é colaborador | Seção 2.2; peça para ser adicionado como colaborador; troque a credencial em *Collaboration Workspace ▸ Properties* |
| Caixas de texto invisíveis na *Primary Password* (Linux) | Wayland / tema GTK customizado | Seção 2.5 |
| Não sei a *Primary Password* | Senha local esquecida | Crie uma nova (*Set new primary password…*) e redigite o token |
| *Publish* rejeitado / "non-fast-forward" | Alguém publicou antes | *Refresh Model*, confira, *Publish Changes* de novo |
| Não vejo a branch de um colega | Ele não publicou, ou você não deu Refresh | Ele faz *Publish*; você faz *Refresh Model* |
| Elemento sumiu da minha view após merge | Alguém apagou na outra branch | *Show Change History* / backup `.archimate`; combine com o grupo |
| Dois elementos iguais (ex.: dois "Cliente") | Criados em branches diferentes | Troque as ocorrências pelo oficial nas views, mova as relações, apague a duplicata |
| Arquivo estranho apareceu no GitHub | Foi colocado na pasta do repositório local | Apague pelo site, adicione o padrão ao `.gitignore` |
| Modelo não abre após merge | XML editado à mão / merge fora do Archi | Restaure o backup ou *Restore to this commit* e refaça o merge pelo Archi |

---

## Resumo

> **Refresh → trabalho na minha branch, nas minhas views → Commit pequeno → Publish → trago a `main` toda
> semana → Validate → Pull Request → integrador faz backup, merge de um PR por vez, valida e cria Release.**
