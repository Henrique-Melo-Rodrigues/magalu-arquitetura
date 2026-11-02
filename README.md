# Magalu – Crédito no Checkout (MagaluPay) · Arquitetura Corporativa (TOGAF + ArchiMate)

Repositório: **<https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura>**

Todos trabalham **no mesmo modelo ArchiMate**, cada um na **sua branch**, e juntamos tudo na `main` por
Pull Request. Ferramentas: **Archi 5.x** + plugin **coArchi** (testado com 0.9.7) + **GitHub**.

> 📌 Primeira vez? Faça as seções **1** e **2** (uma vez só). Depois, o dia a dia é a seção **3**.

---

## Status do projeto

| Fase (pasta de views) | Views | Branch | Status |
|---|---|---|---|
| `0 - preliminar` | Princípios de Arquitetura · Equipe de Arquitetura | `main` | ✅ Concluída |
| `A - Vision` | Stakeholders, Drivers e Objetivos · Realização de Objetivos · Capacidades e Cadeia de Valor · Declaração de Trabalho | `main` | ✅ Concluída |
| `B - Business` | 1. Atores e papéis · 2. Baseline (processo atual 2T26) · 3. Target (processo futuro + capacidades) · 4. Gap analysis | `main` | ✅ Concluída e integrada · 🔍 em revisão final (Henrique) |
| `C - Information Systems` | — | `aluno/<nome>-faseC` | ⏳ A fazer |
| `D - Technology` | — | `aluno/<nome>-faseD` | ⏳ A fazer |
| `E - Opportunities and Solutions` | — | `aluno/<nome>-faseE` | ⏳ A fazer |
| `F - Migration Planning` | — | `aluno/<nome>-faseF` | ⏳ A fazer |

- A Fase B usa dados do **relatório 2T26** da Magalu. O relatório do **3T26 sai em 09/11** e pode gerar
  ajustes no baseline.
- Ordem: **B → C → D → E → F**. **C e D podem andar em paralelo**, mas **reutilizando os elementos de
  negócio da Fase B** (atores, papéis, processos), que já estão na `main`.

**Quem faz o quê** (preencham):

| Aluno | Fase | Branch | Status |
|-------|------|--------|--------|
| Henrique | B – Business | `business` | Integrada · revisão final |
|  |  |  |  |
|  |  |  |  |

---

## 1. Instalação e credenciais (uma vez)

1. Instale o **Archi 5.x**: <https://www.archimatetool.com/download/>
2. Instale o **coArchi**: no Archi, *Help ▸ Manage Plug-ins…* (ou <https://www.archimatetool.com/plugins/>).
   **Todos com a mesma versão** de Archi e coArchi.
3. Mande seu login do GitHub para o Henrique e **aceite o convite de colaborador** (chega por e-mail).
4. Em *Edit ▸ Preferences ▸ Collaboration ▸ General*, preencha **Nome** e **E-mail** (aparecem nos commits).

### Token do GitHub (no lugar da senha)

O GitHub **não aceita a senha da conta**; com ela o Archi dá `TransportException: ... not authorized`.

1. GitHub ▸ sua foto ▸ **Settings** ▸ **Developer settings** ▸ **Personal access tokens** ▸ **Tokens (classic)**.
2. **Generate new token (classic)** · Note: `Archi coArchi - magalu` · Expiration: até o fim do semestre.
3. Marque só o escopo **`repo`** ▸ **Generate token** ▸ **copie na hora** (começa com `ghp_…`, não aparece de novo).

> ⚠️ Tem que ser **classic**. Token *fine-grained* não funciona em repositório de outra pessoa.
> Nunca cole o token em chat, README ou commit.

### Janela "Primary Password" (não é a senha do GitHub)

É uma senha **local, inventada por você**, só para criptografar o token no seu PC.
Deixe *Current* em branco ▸ **Set new primary password…** ▸ digite uma senha nova ▸ **OK**.
Esqueceu? Crie outra e redigite o token.

---

## 2. Baixar o modelo (uma vez)

1. No Archi: **Collaboration ▸ Import Remote Model to Workspace**.
   - URL: `https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura.git`
   - Usuário: **seu login do GitHub** · Senha: **o token** · marque para salvar.
2. O modelo aparece na árvore de Modelos — **é nele que você trabalha**.
3. Abra: **Window ▸ Collaboration Workspace**, **Branches** e **Change History**.
4. Crie sua branch:
   1. **Refresh Model**.
   2. View **Branches** ▸ com `main` selecionada ▸ **Add New Branch to Current Branch** ▸ `aluno/<nome>-<fase>`
      (minúsculas, sem acento, ex.: `aluno/maria-faseC`).
   3. Selecione a branch nova ▸ **Switch Branch**.
   4. **Publish Changes** (para ela existir no GitHub).

> ⚠️ **Não edite o arquivo `.archimate` antigo.** O modelo oficial é o do coArchi.

---

## 3. Dia a dia

```
Refresh Model → modelar → Ctrl+S → Commit Changes → Publish Changes
```

| Ação | O que faz | Quem vê |
|------|-----------|---------|
| **Save** (Ctrl+S) | grava no seu PC | só você |
| **Commit Changes** | registra no histórico local | só você |
| **Publish Changes** | envia ao GitHub | todo o grupo |
| **Refresh Model** | traz o que os outros publicaram na sua branch | — |

- **Publique ao fim de toda sessão** — sem Publish ninguém vê e não há backup.
- Commits pequenos, mensagem clara: `[Fase C] Cria view "Aplicações do Checkout"`.
- Antes de trocar de branch, faça *Commit Changes*.
- Errou? **Abort Uncommitted Changes** (descarta o não commitado) ou **Undo the latest commit** (se ainda não publicou).

### Trazer a `main` para a sua branch (1x por semana e antes do PR)

1. *Commit Changes* do que estiver pendente ▸ **Refresh Model**.
2. View **Branches** ▸ estando na **sua** branch, selecione `main` ▸ **Merge Branch into Current Branch**.
3. Conflito? Veja a seção 5. Depois **Publish Changes**.

---

## 4. Entregar sua parte (Pull Request)

**Checklist:**
- [ ] `main` trazida para minha branch, sem conflito pendente
- [ ] **Tools ▸ Validate Model** sem erros
- [ ] Não dupliquei elementos que já existiam (ex.: dois "Cliente")
- [ ] Não editei views de outros
- [ ] Views na pasta da fase certa, com *Documentation* preenchida
- [ ] *Commit* + *Publish* feitos

Depois: GitHub ▸ **Pull requests ▸ New pull request** ▸ `base: main` ← `compare: sua branch`.
Na descrição, liste as views criadas e os elementos compartilhados que você mexeu. Peça revisão de 1 colega.

O Henrique integra: backup do modelo, **um PR por vez**, *merge commit* (sem squash), valida e avisa o grupo.
Depois de cada merge na `main`, todos fazem **Refresh Model** (e quem está em branch própria traz a `main`).

---

## 5. Conflitos

Conflito = **o mesmo elemento ou a mesma view** alterado nas duas branches. O coArchi lista os objetos e, para
cada um, você escolhe **Ours** (sua versão) ou **Theirs** (a do outro) — não mistura campo a campo.

1. Escolha a versão **mais completa**.
2. Depois do merge, **refaça à mão** o que a outra versão tinha de diferente.
3. *Validate Model*, confira as views e faça o commit.

Na dúvida, **cancele o merge** e chame o colega.

**Nunca:** editar XML à mão (GitHub web, VS Code…) · resolver conflito pelo editor do GitHub ·
`git push --force` · apagar a branch de alguém antes de estar na `main`.

---

## 6. Regras de ouro

1. **Cada um é dono das suas views.** Não mexa na view do outro sem combinar.
2. **Antes de criar um elemento, pesquise na árvore.** Se já existe (`Cliente`, `Magalu`, `MagaluPay`,
   `App Magalu`, atores/processos da Fase B…), **arraste o existente** para a sua view. Criar de novo gera
   duplicata silenciosa.
3. **Não apague nem renomeie elementos que outros usam** sem avisar (apagar remove de todas as views).
4. **Não reorganize as pastas** do modelo.
5. **Refresh antes de começar, Publish ao terminar.**
6. **Não coloque arquivos na pasta do repositório local** (`Documentos\Archi\model-repository\...`):
   o coArchi envia **tudo** que estiver lá. Exportações e `.archimate` de entrega ficam fora dela.
7. README e `.gitignore` só são editados **pelo site do GitHub**, por uma pessoa de cada vez. Nada dentro de
   `model/` ou `images/` é editado fora do Archi.

---

## 7. Problemas comuns

| Problema | Solução |
|----------|---------|
| `TransportException ... not authorized` | Use o **token classic** com escopo `repo`; confirme que aceitou o convite; troque a credencial em *Collaboration Workspace ▸ Properties* |
| Esqueci a *Primary Password* | Crie uma nova e redigite o token |
| *Publish* rejeitado / "non-fast-forward" | Alguém publicou antes: **Refresh Model** e publique de novo |
| Não vejo a branch de um colega | Ele precisa dar *Publish*; você, *Refresh Model* |
| Elemento sumiu da view após merge | Alguém apagou na outra branch: *Show Change History* ▸ *Restore*; combine com o grupo |
| Dois elementos iguais | Troque pelo oficial nas views, mova as relações, apague a duplicata |
| Arquivo estranho no GitHub | Foi parar na pasta do repositório local: apague pelo site e avise o Henrique |
| Modelo não abre após merge | Alguém editou XML à mão: *Restore to this commit* e refaça o merge pelo Archi |

---

> **Resumo: Refresh → modelo na minha branch, nas minhas views → Commit → Publish → trago a `main` toda
> semana → Validate → Pull Request.**
