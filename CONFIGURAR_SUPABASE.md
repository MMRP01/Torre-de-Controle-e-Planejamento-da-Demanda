# Publicar a Torre de Controle de Produção online — guia completo, do zero

Resultado: um endereço na internet que várias pessoas abrem **ao mesmo tempo**, cada uma com o próprio e-mail e senha,
vendo as alterações umas das outras em poucos segundos, sem recarregar.

- A **tela** fica no **GitHub Pages** (grátis).
- Os **dados, o login e o tempo real** ficam no **Supabase** (plano gratuito).

Tempo total: cerca de 40 minutos. Você precisa de um e-mail e de um computador. **Siga na ordem.**

---

## PARTE A — Supabase (o servidor)

### A1. Criar o projeto
1. Entre em **supabase.com** → **Start your project** → crie a conta (pode ser com o GitHub).
2. **New project**. Nome: `producao-menzoil`. Crie uma **senha do banco** e anote-a. Região: **South America (São Paulo)**.
3. Espere 1 a 2 minutos até o projeto ficar pronto.

### A2. Criar as tabelas e as regras de segurança
1. No menu da esquerda, **SQL Editor** → **New query**.
2. Abra o arquivo **`supabase/schema.sql`** deste pacote com o Bloco de Notas, copie **tudo** (Ctrl+A, Ctrl+C), cole no editor e clique em **Run**.
3. Deve aparecer *Success*. (Pode rodar de novo quando quiser: é seguro.)

### A3. Ajustar o login
1. **Authentication → Providers** (ou *Sign In / Providers*): confirme que **Email** está habilitado.
2. **Desmarque "Confirm email"** (confirmar e-mail). Assim, quem criar conta entra direto e o administrador libera depois.
3. **Authentication → URL Configuration → Site URL**: coloque o endereço que o seu site terá (você o descobre na Parte B;
   pode voltar aqui depois): `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`

### A4. Conferir o tempo real
No **SQL Editor**, rode:
```sql
select tablename from public.pg_publication_tables where pubname = 'supabase_realtime';
```
O resultado deve listar **`registros`** e **`perfis`**. Se não listar, rode:
```sql
alter publication supabase_realtime add table public.registros;
alter publication supabase_realtime add table public.perfis;
```
(Se aparecer "already member of publication", já estava certo.)

### A5. Deixar à mão a URL e a chave
No menu da esquerda, **⚙ Project Settings → API** (ou **Data API / API Keys**; ou o botão **Connect** no topo da página do projeto).
- **Project URL** — `https://CODIGO-DO-SEU-PROJETO.supabase.co`
- Chave **`anon` `public`** — texto longo que começa com `eyJ` (em *Legacy API Keys*, se o painel tiver essa aba).
  Use o botão de **copiar**. **Nunca** use a `service_role`.

> Não precisa digitar nada à mão: na Parte C uma página confere os dois valores para você.

---

## PARTE B — GitHub (onde a tela fica publicada)

### B1. Criar o repositório
1. Entre em **github.com** (crie a conta, se não tiver) → **+ → New repository**.
2. Nome: `planejamento-producao`. Marque **Public**. **Não** marque "Add a README". **Create repository**.

### B2. Enviar os arquivos
1. Extraia o `PARA-O-GITHUB_planejamento-producao.zip` no computador.
2. No repositório, clique em **uploading an existing file**.
3. Abra a pasta extraída, selecione **o que está dentro dela** (não a pasta em si) e arraste para a página. Tem de subir
   **todos** estes arquivos: `index.html` · `config.js` · **`supabase.js`** · `configurar.html` · `diagnostico.html` · `README.md` · `.nojekyll`.
   As pastas `docs` e `supabase` são opcionais (só guardam este guia e o SQL). Se o navegador não aceitar arrastar pastas, envie só os arquivos soltos.
4. **Commit changes**.
5. Confira: o **`index.html`** aparece **na primeira tela** do repositório (e não dentro de uma pasta).

### B3. Ligar o GitHub Pages
1. **Settings → Pages**.
2. **Source: Deploy from a branch** · **Branch: `main`** · pasta **`/ (root)`** · **Save**.
3. Em 1 a 2 minutos aparece o endereço: `https://SEU-USUARIO.github.io/planejamento-producao/`. **Anote.**
4. Volte à etapa **A3.3** e coloque esse endereço em *Site URL* do Supabase.

---

## PARTE C — Ligar a tela ao servidor

### C1. Gerar o `config.js` certo (sem editar nada à mão)
1. Abra `https://SEU-USUARIO.github.io/planejamento-producao/configurar.html`.
2. Cole a **Project URL** e a chave **anon public** (da etapa A5) e clique em **Testar e gerar o config.js**.
3. A página **testa o servidor de verdade**. Se estiver tudo certo, mostra **"✓ Conexão com o servidor confirmada"** e o texto
   pronto do `config.js`. Se algo estiver errado (URL de exemplo, chave secreta, chave de outro projeto, projeto pausado…), ela diz o quê.
4. No GitHub: clique em **config.js** → ícone do **lápis** → apague **todo** o conteúdo → cole o texto gerado → **Commit changes**.
   (Alternativa: **Baixar config.js** e substituir o arquivo com *Add file → Upload files*.)

> O `config.js` que vem no pacote está **em branco de propósito**. A URL `abcdefghijkl.supabase.co` que aparece nos
> comentários é só um exemplo: a ferramenta a recusa e avisa.

### C2. Abrir o site
1. Espere 1 a 2 minutos e abra `https://SEU-USUARIO.github.io/planejamento-producao/` com **Ctrl + F5**.
2. Deve aparecer a tela de **Entrar** (**E-mail** e **Senha**), com **"Criar conta"** e **"Esqueci a senha"**, e no rodapé
   **"versão 2026-10-29.3"**.

### C3. Criar a sua conta (faça isso ANTES de divulgar o endereço)
1. Clique em **Criar conta** → nome, e-mail, senha.
2. **A primeira conta criada vira administradora automaticamente.**

### C4. Testar tudo
1. No menu: **Usuários e Permissões → 🩺 Testar conexão**. Todos os passos com **✓** (login, leitura, gravação, tempo real, presença, perfis).
2. Se algum falhar, a própria tela diz o que fazer. Você também pode abrir `.../diagnostico.html` e clicar em **Executar diagnóstico**.

---

## PARTE D — Dados e pessoas

### D1. Colocar os seus dados no servidor (uma vez)
Escolha uma opção:
- **A) Enviar o arquivo completo (recomendado).** Copie o **`config.js` já preenchido** para a mesma pasta do **`index.html` completo**
  (o do zip *PRIVADO*), abra esse `index.html` no navegador e entre como administrador. Como o servidor está vazio, a ferramenta pergunta
  *"Enviar esses dados ao servidor?"* → **Confirmar**. (Itens, receitas e pedidos sobem em segundos.)
- **B) Importar planilhas** pelo site (*Importação de Dados*) e cadastrar os recursos.
- **C) Restaurar um backup (.json)** em *Importação de Dados*.

### D2. Adicionar as pessoas
1. A pessoa abre o endereço e clica em **Criar conta**.
2. A conta aparece na hora em *Usuários e Permissões* como **⏳ Aguardando liberação**.
3. Você clica **Liberar** e define o que ela vê e edita (por tela, por campo e, se quiser, **trava de filtros**).
4. Mudanças de permissão chegam à pessoa **ao vivo**. **Desativar** derruba a sessão dela na hora.

### D3. Teste de simultaneidade (2 minutos)
1. Abra o site em **dois navegadores diferentes** (ou um normal e um anônimo), com **duas contas** liberadas, ambas com *Edição* na Lista Mestre.
2. Na barra lateral, os dois devem mostrar **"● Online · 2 conectados"**.
3. No navegador 1, na **Lista Mestre**, digite algo no **Nº OP** de uma linha e saia do campo.
4. No navegador 2, o valor aparece **sozinho**, com o aviso "🔄 Fulano atualizou 1 registro".
5. Se não aparecer, clique em **"● Online"** na barra lateral (atualiza na hora) e rode **🩺 Testar conexão**.

---

## Como o trabalho simultâneo funciona
- Cada alteração é enviada em segundos e aparece nas outras telas abertas. Quem está digitando não é interrompido.
- Duas pessoas em **campos diferentes** do mesmo registro: as duas alterações valem. No **mesmo campo**: vale a última gravação.
- **Se o tempo real do servidor não funcionar**, a ferramenta percebe e passa a buscar as mudanças a cada poucos segundos
  ("● Online · atualiza a cada 5 s"). Só não é instantâneo.
- **Sem internet:** aparece "⚠ Sem conexão — N alteração(ões) aguardando"; ao voltar, a ferramenta envia o que ficou pendente e baixa o que perdeu.
- O servidor **recusa** gravação de quem só tem leitura e a mudança de programação de linha que já tem produção (só administrador).
- **Gerar plano** mexe em muitas linhas: evite que duas pessoas gerem o plano ao mesmo tempo.

## Quando algo dá errado
| O que aparece | Causa provável | O que fazer |
|---|---|---|
| "O config.js ainda está com a URL ou a chave de EXEMPLO" | Os valores de exemplo não foram trocados | Use o `configurar.html` (C1) |
| "Não conseguiu falar com o servidor xxxx.supabase.co" | URL errada (a causa mais comum), projeto **pausado**, ou bloqueio de rede | Gere o `config.js` de novo no `configurar.html`; no painel, *Restore project* se estiver pausado |
| "O servidor respondeu, mas recusou a chave" | Chave incompleta, ou de outro projeto | Copie de novo a **anon public** (botão de copiar), do mesmo projeto |
| "A chave colocada é a service_role" | Colou a chave **secreta** | Use a **anon public** e gere uma nova `service_role` no painel (a antiga foi exposta) |
| "Não foi possível carregar a biblioteca de conexão" | O `supabase.js` não foi enviado ao GitHub | Suba o `supabase.js` na mesma pasta do `index.html` |
| Abre o login antigo, com "Usuário" em vez de "E-mail" | `config.js` publicado em branco | Refaça a etapa C1 |
| Funciona para você mas não para outras pessoas | Cópia antiga em cache; ou `config.js` diferente do que você usa | Peça **Ctrl+F5**; peça para abrirem `.../diagnostico.html`, **Executar diagnóstico**, **Copiar relatório** e enviarem a você |
| Conta criada, mas "Aguardando liberação" | É o esperado | O administrador libera em *Usuários e Permissões* |
| Alterações só aparecem para o outro depois de um tempo | Tempo real desligado (usando a atualização de reserva) | Etapa A4 e 🩺 Testar conexão |
| "2 conectados" não aparece | Tempo real/presença desligado | Etapa A4 |
| Link de "Esqueci a senha" abre página errada | *Site URL* errada no Supabase | Etapa A3.3 |
| "Confirme o e-mail primeiro" | "Confirm email" está ligado | Etapa A3.2 |
| Não deixa rebaixar um administrador | Regra de segurança: sempre existe um administrador ativo | Promova outro antes |
| Projeto "pausado" | O plano gratuito pausa após cerca de 1 semana sem uso | No painel, *Restore project* |

## Atualizar a ferramenta depois
Em **Add file → Upload files**, envie o `index.html` (e `supabase.js`, `diagnostico.html`, `configurar.html`) novos.
**Não envie o `config.js` do pacote** (ele vem em branco e apagaria o seu). Exporte um **backup** antes.

## Domínio próprio (opcional)
*Settings → Pages → Custom domain*; no provedor do domínio, um registro **CNAME** (subdomínio) para `SEU-USUARIO.github.io`.
Marque **Enforce HTTPS** e atualize o *Site URL* do Supabase.

## Backup, custo e segurança
- **Backup:** o plano gratuito não tem backup automático com retorno no tempo. Use **Importação de Dados → Exportar backup**
  com frequência e guarde o arquivo **fora do GitHub** (tem dados reais).
- **Custo:** o gratuito atende bem uma equipe pequena; confira os limites atuais no site do Supabase.
- **Segurança:** só quem está logado **e ativo** lê os dados; ninguém grava direto nas tabelas (só pela função do servidor, que
  confere permissão, versão e a trava de linha produzida). Campos por tela e travas de filtro organizam o uso. A chave `anon`
  pode ficar no GitHub; **a `service_role` nunca**.
- **LGPD:** os dados ficam no Supabase, na região escolhida. Trate o acesso ao painel e a senha do banco como confidenciais.
