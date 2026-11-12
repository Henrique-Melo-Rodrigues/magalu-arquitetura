# Magalu – Crédito no Checkout (MagaluPay) · Arquitetura Corporativa (TOGAF + ArchiMate)

Repositório: **<https://github.com/Henrique-Melo-Rodrigues/magalu-arquitetura>**

Todos trabalham **no mesmo modelo ArchiMate**, numa única branch de trabalho, a **`business`**, e juntamos
tudo na `main` por Pull Request. Ferramentas: **Archi 5.x** + plugin **coArchi** (testado com 0.9.7) + **GitHub**.

> ✅ **Ciclo ADM concluído até a Fase F (Migration Planning).** Modelo final: 240 elementos, 564 relações e
> 36 views.

> 📌 Primeira vez? Faça as seções **1** e **2** (uma vez só). Depois, o dia a dia é a seção **3**.

---

## Status do projeto

| Fase (pasta de views) | Views | Responsável | Status |
|---|---|---|---|
| `0 - preliminar` | Princípios de Arquitetura · Equipe de Arquitetura | Nicolas Tamashiro | ✅ Concluída |
| `A - Vision` | Stakeholders, Drivers e Objetivos · Realização de Objetivos · Capacidades e Cadeia de Valor · Declaração de Trabalho | Nicolas Tamashiro | ✅ Concluída (revisada após a devolutiva do professor, metas OE) |
| `B - Business` | Atores e papéis · Baseline (2T26) · Target (processo futuro e capacidades) · Gap analysis · Rastreabilidade com a Vision | Henrique Rodrigues | ✅ Concluída |
| `C - Information Systems` | C1 a C7: dados conceitual e lógico · aplicação baseline e target · acesso aos dados · rastreabilidade · gap analysis | Pedro Henrique Fernandes | ✅ Concluída |
| `D - Technology` | D1 a D7: baseline · target (infraestrutura e nuvem) · implantação · dados · serviços · rastreabilidade · gap analysis | João Pedro | ✅ Concluída |
| `E - Opportunities and Solutions` | E1 a E5: gaps e pacotes · roadmap (plateaus) · cronograma · dependências · riscos | Paulo Pimenta | ✅ Concluída |
| `F - Migration Planning` | F1 a F4: cobertura dos gaps · priorização · plano de implementação (ondas e marcos) · governança | Nicolas Tamashiro; revisão de Nicolas Tamashiro e Henrique Rodrigues | ✅ Concluída |
| *(raiz de Views)* | **Visão integrada - todas as fases do ADM** | Iniciada por Nicolas Tamashiro e finalizada por Henrique Rodrigues | ✅ Concluída |

- **Visão integrada:** pedida pelo professor, porque é padrão em projetos Archi ter uma view geral com o modelo
  inteiro, e não só views menores separadas por fase. Ela mostra, num só desenho, objetivo → requisito →
  processo → aplicação → tecnologia → transição. A fundamentação detalhada continua nas views de cada fase.
- A Fase B usa dados do **relatório 2T26** da Magalu.
- Ordem seguida: **B → C → D → E → F**. As fases G e H não foram modeladas.

> ℹ️ **Por que só a branch `business`.** O plano inicial previa uma branch por aluno e por fase
> (`aluno/<nome>-<fase>`). Na prática, o fluxo do coArchi não foi seguido à risca: cada fase foi modelada em um
> arquivo `.archimate` separado e importada na `business` (seção 3). Por isso as branches por aluno deixaram de
> ser necessárias.

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
2. O modelo aparece na árvore de Modelos. **É nele que você trabalha.**
3. Abra: **Window ▸ Collaboration Workspace**, **Branches** e **Change History**.
4. Na view **Branches**, selecione **`business`** ▸ **Switch Branch** ▸ **Refresh Model**.

> ⚠️ Um `.archimate` aberto por *File ▸ Open* **não** é ligado ao repositório: nele, *Commit* e *Publish*
> ficam desabilitados. O modelo oficial é o do **Collaboration Workspace**.

---

## 3. Dia a dia (na `business`)

```
Refresh Model → modelar (ou importar seu .archimate) → Ctrl+S → Commit Changes → Publish Changes
```

| Ação | O que faz | Quem vê |
|------|-----------|---------|
| **Save** (Ctrl+S) | grava no seu PC | só você |
| **Commit Changes** | registra no histórico local | só você |
| **Publish Changes** | envia ao GitHub | todo o grupo |
| **Refresh Model** | traz o que os outros publicaram na `business` | — |

- **Publique ao fim de toda sessão.** Sem Publish, ninguém vê e não há backup.
- Commits pequenos, mensagem clara: `[Fase C] Cria view "Aplicações do Checkout"`.
- **Nunca modele direto na `main`.**
- Errou? **Abort Uncommitted Changes** (descarta o não commitado) ou **Undo the latest commit** (se ainda não publicou).

### Levar uma fase feita num `.archimate` separado

1. Feche o `.archimate` da fase, se estiver aberto.
2. Selecione o modelo do repositório na árvore ▸ **File ▸ Import ▸ Another Model Into Selected Model…** ▸ escolha
   o arquivo. Marque **Update existing objects and folders**.
3. **Antes de salvar**, confira a árvore: não pode haver pasta ou elemento em dobro. Se houver, use **Close Model**
   e responda **No** para não salvar (seção 7).
4. **Tools ▸ Validate Model** ▸ **Ctrl+S** ▸ **Commit Changes** ▸ **Publish Changes**.

### Trazer a `main` para a `business` (depois de cada merge e antes do PR)

1. *Commit Changes* do que estiver pendente ▸ **Refresh Model**.
2. View **Branches** ▸ estando na `business`, selecione `main` ▸ **Merge Branch into Current Branch**.
3. Conflito? Veja a seção 5. Depois **Publish Changes**.

---

## 4. Entregar (Pull Request `business → main`)

**Checklist:**
- [ ] `main` trazida para a `business`, sem conflito pendente
- [ ] **Tools ▸ Validate Model** sem erros
- [ ] Não dupliquei elementos nem pastas que já existiam (ex.: dois "Cliente", duas "B - Business")
- [ ] Não editei views de outros
- [ ] Views na pasta da fase certa, com *Documentation* preenchida
- [ ] *Commit* + *Publish* feitos

Depois: GitHub ▸ **Pull requests ▸ New pull request** ▸ `base: main` ← `compare: business`.
Na descrição, liste as views criadas e os elementos compartilhados que você mexeu. Peça revisão de 1 colega.

O Henrique integra: backup do modelo, *merge commit* (sem squash), valida e avisa o grupo.
Depois de cada merge, todos fazem **Refresh Model** e trazem a `main` para a `business`.

---

## 5. Conflitos

Conflito = **o mesmo elemento ou a mesma view** alterado na `business` e na `main`. O coArchi lista os objetos e,
para cada um, você escolhe **Ours** (sua versão) ou **Theirs** (a do outro). Ele não mistura campo a campo.

1. Escolha a versão **mais completa**.
2. Depois do merge, **refaça à mão** o que a outra versão tinha de diferente.
3. *Validate Model*, confira as views e faça o commit.

Na dúvida, **cancele o merge** e chame o grupo.

**Nunca:** editar XML à mão (GitHub web, VS Code…) · resolver conflito pelo editor do GitHub ·
`git push --force` · apagar a `business`.

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
| *Commit* e *Publish* desabilitados | O `.archimate` foi aberto por *File ▸ Open*: abra o modelo do **Collaboration Workspace** e importe o arquivo nele (seção 3) |
| Pastas duplicadas depois de importar | O arquivo veio de um XML *Open Exchange*, que não guarda o ID das pastas: **Close Model** sem salvar, alinhe os IDs das pastas com os do repositório e importe de novo |
| *Publish* rejeitado / "non-fast-forward" | Alguém publicou antes: **Refresh Model** e publique de novo |
| Elemento sumiu da view após merge | Alguém apagou: *Show Change History* ▸ *Restore*; combine com o grupo |
| Dois elementos iguais | Troque pelo oficial nas views, mova as relações, apague a duplicata |
| Arquivo estranho no GitHub | Foi parar na pasta do repositório local: apague pelo site e avise o Henrique |
| Modelo não abre após merge | Alguém editou XML à mão: *Restore to this commit* e refaça o merge pelo Archi |

---

> **Resumo: Refresh → trabalho na `business`, nas minhas views (ou importo meu `.archimate`) → confiro
> duplicatas → Validate → Commit → Publish → Pull Request `business → main` → trago a `main` de volta.**
