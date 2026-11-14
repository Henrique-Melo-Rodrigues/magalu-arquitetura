# Magalu – Crédito no Checkout (MagaluPay) · Arquitetura Corporativa (TOGAF + ArchiMate)


O grupo trabalhou **no mesmo modelo ArchiMate**, versionado no GitHub com o plugin **coArchi**. Todo o trabalho
foi feito numa única branch, a **`business`**, e consolidado na `main` por Pull Request.
Ferramentas: **Archi 5.x** + **coArchi** (testado com 0.9.7) + **GitHub**.

> ✅ **Projeto concluído.** O ciclo ADM foi modelado da Fase Preliminar até a Fase F (Migration Planning).
> A `main` contém a versão final e o modelo não recebe mais alterações. Modelo final: 240 elementos,
> 564 relações e 36 views.

---

## Como abrir o modelo

- **Pelo arquivo:** abra o `.archimate` de entrega no Archi com *File ▸ Open*.
- **Pelo repositório:** no Archi com o coArchi instalado, use **Collaboration ▸ Import Remote Model to Workspace**
  com a URL `https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura.git` e escolha a branch `main`.
  Assim dá para ver também o histórico de commits de cada fase (*Change History*).
- **Pelo navegador:** a pasta `model/` tem um XML por elemento, relação e view, e o histórico de commits mostra
  a evolução do modelo fase a fase.

---

## Status final

| Fase (pasta de views) | Views | Responsável | Status |
|---|---|---|---|
| `0 - preliminar` | Princípios de Arquitetura · Equipe de Arquitetura | Nicolas Tamashiro | ✅ Concluída (layout refinado na versão final) |
| `A - Vision` | Stakeholders, Drivers e Objetivos · Realização de Objetivos · Capacidades e Cadeia de Valor · Declaração de Trabalho | Nicolas Tamashiro | ✅ Concluída (revisada após a devolutiva do professor, metas OE; layout refinado na versão final) |
| `B - Business` | Atores e papéis · Baseline (2T26) · Target (processo futuro e capacidades) · Gap analysis · Rastreabilidade com a Vision | Henrique Rodrigues | ✅ Concluída |
| `C - Information Systems` | C1 a C7: dados conceitual e lógico · aplicação baseline e target · acesso aos dados · rastreabilidade · gap analysis | Pedro Henrique Fernandes | ✅ Concluída |
| `D - Technology` | D1 a D7: baseline · target (infraestrutura e nuvem) · implantação · dados · serviços · rastreabilidade · gap analysis | João Pedro | ✅ Concluída |
| `E - Opportunities and Solutions` | E1 a E5: gaps e pacotes · roadmap (plateaus) · cronograma · dependências · riscos | Paulo Pimenta | ✅ Concluída |
| `F - Migration Planning` | F1 a F4: cobertura dos gaps · priorização · plano de implementação (ondas e marcos) · governança | Nicolas Tamashiro; revisão de Nicolas Tamashiro e Henrique Rodrigues | ✅ Concluída |
| *(raiz de Views)* | **Visão integrada - todas as fases do ADM** | Iniciada por Nicolas Tamashiro e finalizada por Henrique Rodrigues | ✅ Concluída |

- **Visão integrada:** pedida pelo professor, porque é padrão em projetos Archi ter uma view geral com o modelo
  inteiro, e não só views menores separadas por fase. Ela mostra, num só desenho, objetivo → requisito →
  processo → aplicação → tecnologia → transição. A fundamentação detalhada está nas views de cada fase.
- A Fase B usou dados do **relatório 2T26** da Magalu.
- Ordem seguida: **B → C → D → E → F**. As fases G e H ficaram fora do escopo.

> ℹ️ **Por que só a branch `business`.** O plano inicial previa uma branch por aluno e por fase
> (`aluno/<nome>-<fase>`). Na prática, cada fase foi modelada em um arquivo `.archimate` separado e importada
> na `business` (seção 3). Por isso as branches por aluno não foram necessárias.

---

## Fluxo de trabalho adotado

As seções abaixo registram como o grupo usou o Archi, o coArchi e o GitHub durante o projeto.
Ficam como referência para quem quiser repetir o processo.

## 1. Instalação e credenciais

1. Instalar o **Archi 5.x**: <https://www.archimatetool.com/download/>
2. Instalar o **coArchi**: no Archi, *Help ▸ Manage Plug-ins…* (ou <https://www.archimatetool.com/plugins/>).
   **Todos com a mesma versão** de Archi e coArchi.
3. Cada integrante foi adicionado como colaborador do repositório (convite por e-mail).
4. Em *Edit ▸ Preferences ▸ Collaboration ▸ General*, preencher **Nome** e **E-mail** (aparecem nos commits).

### Token do GitHub (no lugar da senha)

O GitHub **não aceita a senha da conta**; com ela o Archi dá `TransportException: ... not authorized`.

1. GitHub ▸ foto ▸ **Settings** ▸ **Developer settings** ▸ **Personal access tokens** ▸ **Tokens (classic)**.
2. **Generate new token (classic)** · Note: `Archi coArchi - magalu` · Expiration: até o fim do semestre.
3. Marcar só o escopo **`repo`** ▸ **Generate token** ▸ **copiar na hora** (começa com `ghp_…`, não aparece de novo).

> ⚠️ Tem que ser **classic**. Token *fine-grained* não funciona em repositório de outra pessoa.
> Nunca cole o token em chat, README ou commit.

### Janela "Primary Password" (não é a senha do GitHub)

É uma senha **local, inventada por você**, só para criptografar o token no seu PC.
Deixe *Current* em branco ▸ **Set new primary password…** ▸ digite uma senha nova ▸ **OK**.
Esqueceu? Crie outra e redigite o token.

---

## 2. Baixar o modelo

1. No Archi: **Collaboration ▸ Import Remote Model to Workspace**.
   - URL: `https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura.git`
   - Usuário: **login do GitHub** · Senha: **o token** · marcar para salvar.
2. O modelo aparece na árvore de Modelos. **Era nele que cada um trabalhava.**
3. Abrir: **Window ▸ Collaboration Workspace**, **Branches** e **Change History**.
4. Na view **Branches**, selecionar **`business`** ▸ **Switch Branch** ▸ **Refresh Model**.

> ⚠️ Um `.archimate` aberto por *File ▸ Open* **não** é ligado ao repositório: nele, *Commit* e *Publish*
> ficam desabilitados. O modelo oficial é o do **Collaboration Workspace**.

---

## 3. Dia a dia (na `business`)

```
Refresh Model → modelar (ou importar o .archimate da fase) → Ctrl+S → Commit Changes → Publish Changes
```

| Ação | O que faz | Quem vê |
|------|-----------|---------|
| **Save** (Ctrl+S) | grava no PC | só você |
| **Commit Changes** | registra no histórico local | só você |
| **Publish Changes** | envia ao GitHub | todo o grupo |
| **Refresh Model** | traz o que os outros publicaram na `business` | — |

- **Publicar ao fim de toda sessão.** Sem Publish, ninguém vê e não há backup.
- Commits pequenos, mensagem clara: `[Fase C] Cria view "Aplicações do Checkout"`.
- **Nunca modelar direto na `main`.**
- Errou? **Abort Uncommitted Changes** (descarta o não commitado) ou **Undo the latest commit** (se ainda não publicou).

### Levar uma fase feita num `.archimate` separado

1. Fechar o `.archimate` da fase, se estiver aberto. **Deixar aberto só o modelo do repositório.**
2. Selecionar o modelo do repositório na árvore ▸ **File ▸ Import ▸ Another Model Into Selected Model…** ▸ escolher
   o arquivo. Marcar **Update existing objects and folders**.
3. **Antes de salvar**, conferir a árvore: não pode haver pasta ou elemento em dobro. Se houver, **Close Model**
   e responder **No** para não salvar (seção 7).
4. **Tools ▸ Validate Model** ▸ **Ctrl+S** ▸ **Commit Changes** ▸ **Publish Changes**.

> 💡 Se a fase veio como **XML Open Exchange**, o `.archimate` gerado a partir dele perde os IDs das pastas.
> Antes de importar, é preciso alinhar esses IDs com os do repositório, senão as pastas duplicam (seção 7).

### Trazer a `main` para a `business` (depois de cada merge e antes do PR)

1. *Commit Changes* do que estiver pendente ▸ **Refresh Model**.
2. View **Branches** ▸ estando na `business`, selecionar `main` ▸ **Merge Branch into Current Branch**.
3. Conflito? Ver a seção 5. Depois **Publish Changes**.

---

## 4. Entrega por Pull Request (`business → main`)

**Checklist usado antes de cada PR:**
- [x] `main` trazida para a `business`, sem conflito pendente
- [x] **Tools ▸ Validate Model** sem erros
- [x] Nenhum elemento ou pasta duplicado (ex.: dois "Cliente", duas "B - Business")
- [x] Nenhuma view de outro integrante editada sem combinar
- [x] Views na pasta da fase certa, com *Documentation* preenchida
- [x] *Commit* + *Publish* feitos

Depois: GitHub ▸ **Pull requests ▸ New pull request** ▸ `base: main` ← `compare: business`.
Na descrição, a lista das views criadas e dos elementos compartilhados alterados, com revisão de 1 colega.

O Henrique integrava: backup do modelo, *merge commit* (sem squash), validação e aviso ao grupo.
Depois de cada merge, todos faziam **Refresh Model** e traziam a `main` para a `business`.

---

## 5. Conflitos

Conflito = **o mesmo elemento ou a mesma view** alterado na `business` e na `main`. O coArchi lista os objetos e,
para cada um, você escolhe **Ours** (sua versão) ou **Theirs** (a do outro). Ele não mistura campo a campo.

1. Escolher a versão **mais completa**.
2. Depois do merge, **refazer à mão** o que a outra versão tinha de diferente.
3. *Validate Model*, conferir as views e fazer o commit.

Na dúvida, **cancelar o merge** e chamar o grupo.

**Nunca:** editar XML à mão (GitHub web, VS Code…) · resolver conflito pelo editor do GitHub ·
`git push --force` · apagar a `business`.

---

## 6. Regras de ouro

1. **Cada um é dono das suas views.** Nada de mexer na view do outro sem combinar.
2. **Antes de criar um elemento, pesquisar na árvore.** Se já existe (`Cliente`, `Magalu`, `MagaluPay`,
   `App Magalu`, atores/processos da Fase B…), **arrastar o existente** para a view. Criar de novo gera
   duplicata silenciosa.
3. **Não apagar nem renomear elementos que outros usam** sem avisar (apagar remove de todas as views).
4. **Não reorganizar as pastas** do modelo.
5. **Refresh antes de começar, Publish ao terminar.**
6. **Nenhum arquivo extra na pasta do repositório local** (`Documentos\Archi\model-repository\...`):
   o coArchi envia **tudo** que estiver lá. Exportações e `.archimate` de entrega ficam fora dela.
7. README e `.gitignore` só são editados **pelo site do GitHub**, por uma pessoa de cada vez. Nada dentro de
   `model/` ou `images/` é editado fora do Archi.

---

## 7. Problemas comuns

| Problema | Solução |
|----------|---------|
| `TransportException ... not authorized` | Usar o **token classic** com escopo `repo`; confirmar que o convite foi aceito; trocar a credencial em *Collaboration Workspace ▸ Properties* |
| Esqueci a *Primary Password* | Criar uma nova e redigitar o token |
| *Commit* e *Publish* desabilitados | O `.archimate` foi aberto por *File ▸ Open*: abrir o modelo do **Collaboration Workspace** e importar o arquivo nele (seção 3) |
| *Nothing to commit* logo depois de importar | O modelo não foi salvo (ainda tem `*` no nome): **Ctrl+S** com o modelo do repositório selecionado e tentar de novo |
| Dois modelos com o mesmo nome na árvore | O `.archimate` da fase continua aberto e o Ctrl+S pode ir para ele: fechar os dois, reabrir só o do **Collaboration Workspace** e importar de novo |
| Pastas duplicadas depois de importar | O arquivo veio de um XML *Open Exchange*, que não guarda o ID das pastas: **Close Model** sem salvar, alinhar os IDs das pastas com os do repositório e importar de novo |
| *Publish* rejeitado / "non-fast-forward" | Alguém publicou antes: **Refresh Model** e publicar de novo |
| Elemento sumiu da view após merge | Alguém apagou: *Show Change History* ▸ *Restore*; combinar com o grupo |
| Dois elementos iguais | Trocar pelo oficial nas views, mover as relações, apagar a duplicata |
| Arquivo estranho no GitHub | Foi parar na pasta do repositório local: apagar pelo site e avisar o Henrique |
| Modelo não abre após merge | Alguém editou XML à mão: *Restore to this commit* e refazer o merge pelo Archi |

---

> **Resumo do fluxo: Refresh → trabalho na `business`, cada um nas suas views (ou importando o `.archimate` da
> fase) → conferência de duplicatas → Validate → Commit → Publish → Pull Request `business → main` → `main`
> trazida de volta para a `business`.**
