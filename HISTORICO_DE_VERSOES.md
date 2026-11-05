# Histórico de versões

A versão aparece no rodapé da tela de entrada ("versão AAAA-MM-DD.N") e no relatório do `diagnostico.html`.
Para atualizar a ferramenta publicada sem perder dados, veja "Atualizar a ferramenta depois" em `CONFIGURAR_SUPABASE.md`.

## 2026-11-05.4
- **Reimportar a base de pedidos não devolve mais o planejado para "pendente".** A pendência de um pedido é o que ele pede menos o que as linhas do plano (planejadas e
  produzidas) já cobrem, e as linhas apontam para o pedido pelo **id**. As importações (tanto "atualizar" quanto "substituir toda a base") **recriavam os pedidos com
  ids novos**, e com isso todas as linhas perdiam o vínculo e tudo voltava como pendente no Plano Mestre. Agora os pedidos que já existiam **mantêm o mesmo id**
  (casando por número do pedido + item + lote; se o lote mudou, por número do pedido + item), então o que já foi planejado e produzido **continua abatendo**, e só a
  diferença de quantidade (para mais) fica pendente. O relatório da importação informa quantos pedidos mantiveram as linhas do plano.
- **Reparo automático dos dados já quebrados.** Ao abrir a ferramenta, ao restaurar um backup e ao carregar do servidor, as linhas cujo pedido tinha sido recriado por
  uma importação antiga são **reatadas pelo número do pedido + item (+ lote)**. Aparece o aviso "Vínculos reatados: N linha(s)…". Linhas cujo pedido não está mais na
  base ficam como estão.
- Não exige mudança no servidor.

## 2026-11-05.3
- **Lote máximo por cliente, em uma lista que você mantém.** Em **Cadastros → Itens** há o cartão **"Clientes que dividem pelo lote máximo"**: marque os clientes
  cujos pedidos devem ser divididos em linhas pela Capacidade Máxima do Lote (geração do plano, planejar pedido, adicionar linha, reprogramar e o teto na edição de
  quantidade). Para os clientes **não marcados**, a quantidade de um item na mesma data e recurso fica em **uma linha só** (a soma). Antes isso estava fixo no cliente
  MOTUL; **enquanto ninguém editar a lista, continua valendo o MOTUL** (padrão). A lista vazia significa que ninguém divide. A mudança vale para os próximos
  planejamentos; as linhas que já existem não são refeitas. O cartão mostra, por cliente, os pedidos em aberto e os itens sem Capacidade Máxima. A lista é
  **compartilhada entre os usuários** (não exige mudança no servidor) e tem **permissão própria** ("Clientes que dividem pelo lote máximo", em Cadastros).

## 2026-11-05.2
- **Comentários / Observações na linha da Lista Mestre.** Cada linha tem o botão **"Obs."**; ao clicar abre a janela para escrever a observação (com item, data e
  quantidade da linha), e a ferramenta guarda **quem escreveu e quando**. Linha com observação fica **evidente para os operadores**: fundo amarelo na linha, botão **📝 amarelo**
  e em negrito (com o texto ao passar o mouse) e o texto da observação **sai na impressão** da Lista Mestre, junto do item. Quem só consulta abre e lê, mas não grava.
  **Permissão nova** por usuário: campo "Comentários / Observações" (Lista Mestre).
- **Lote máximo só para o cliente MOTUL.** A Capacidade Máxima do Lote passou a dividir as linhas **somente dos itens do cliente MOTUL** (geração do plano, planejar pedido,
  adicionar linha, reprogramar pendência e edição de quantidade). Para os **demais clientes**, a quantidade de um item na mesma data e recurso fica em **uma linha só** (a soma),
  sem teto de lote máximo. Em um item com pedidos dos dois tipos, as linhas não se misturam (cada linha só se vincula a pedidos da sua classe). O Cadastro de Itens avisa os itens com
  pedido do MOTUL sem Capacidade Máxima do Lote.
- **Adicionar linha direto na Lista Mestre, escolhendo o ITEM.** A lista é de **itens** com pedido em aberto (sem pedido: desabilitado, "sem pedido disponível"). O **vínculo com o(s)
  pedido(s) é automático**, do mais antigo para o mais novo; se o item não tiver pedido em aberto, **a inserção não é liberada** (nem para o administrador). A quantidade acima do em aberto
  continua exigindo administrador ou a permissão própria. Quantidade igual ao em aberto é sugerida, e o recurso do item é preenchido.
- **Correção:** o índice interno de itens não era atualizado quando a lista de itens era trocada por outra do mesmo tamanho (ex.: ao restaurar um backup), e a ferramenta podia usar dados
  antigos do item (recurso, litros por unidade, capacidade).
- Não exige mudança no servidor além da já exigida pela versão 2026-11-04.1.

## 2026-11-05.1
- **Lista Mestre — filtros por coluna.** O cabeçalho da tabela ganhou uma **linha de filtros**, logo abaixo dos títulos: campo de **texto** em Item, Descrição, Pedido,
  Lote(s), Nº OP e Nº OP Granel (sem diferenciar maiúsculas nem acentos) e **lista de opções** em Data, Recurso, Contaminante, Localização do Granel e Status. Os filtros
  das colunas **somam-se** aos filtros do topo e valem também para o **resumo por recurso** e para a **impressão**. Os campos ativos ficam destacados e o botão **✕ N**
  limpa todos; "Limpar filtros" do topo também os limpa. Ao digitar, o campo mantém o foco e o cursor. A linha de filtros acompanha as colunas congeladas (Data, Item e
  Descrição) e fica logo abaixo dos títulos ao rolar.
- Não exige mudança no servidor além da já exigida pela versão 2026-11-04.1.

## 2026-11-04.3
- **Solicitar ordem de produção — excluir linhas antes de gerar.** Na janela, cada item tem uma **caixa** para incluir ou excluir (marcada por padrão) e uma **seta**
  que mostra as linhas do plano daquele item, cada uma com a sua caixa. O resumo, a tabela e o registro consideram só o que ficou marcado; é possível **restaurar** as
  excluídas. A solicitação guarda quantas linhas foram excluídas, e só as incluídas recebem a marca de solicitadas.
- **Desmarcar o selo "OP solicitada" de uma linha.** O selo ganhou um **✕**: ele tira a marca daquela linha (que volta a poder entrar em uma nova solicitação) e registra
  quem desmarcou, sem cancelar a solicitação. **Nova permissão por tela** ("Desmarcar OP solicitada") nas telas Itens por Dia, Lista Mestre e Plano Mestre, separada da
  de solicitar.
- **Impressão da Lista Mestre:** **sem a coluna Pedido** e com o **mesmo agrupamento da Lista Mestre**: ordem por Nº OP Granel, depois recurso e data, com a faixa de
  cabeçalho a cada novo Nº OP Granel (linhas, itens e o aviso "Este granel compõe mais de um item"). Data e Recurso passam a ser colunas (não há mais um bloco e uma
  página por dia).
- Não exige mudança no servidor além da já exigida pela versão 2026-11-04.1.

## 2026-11-04.2
- **Totalizador (Dashboards):** novas colunas **1º, 2º e 3º turno (L)** (volume efetuado por turno) nas tabelas "Por recurso" e "Por unidade de medida", e a coluna
  **Horas paradas** nas três tabelas (as paradas são registradas por recurso: por unidade de medida e por turno aparece "—"; a linha Total soma todas). A exportação
  CSV do Dashboard também traz as colunas novas.
- **Colunas congeladas:** nas tabelas largas (que rolam para o lado), as colunas de código e descrição ficam sempre à vista, junto com o cabeçalho: Lista Mestre
  (Data, Item e Descrição), Itens por Dia e Planejado x Efetuado (Nº do item e Descrição), Necessidades (Código e Insumo), Cadastro de Itens (Código e Descrição),
  Pedidos & Lead Time (Pedido e Cliente), Produção diária do Dashboard (Recurso e Total) e Planejamento de Materiais (Material).
- **Solicitar ordem de produção:** o relatório (tabela da janela, impressão e CSV) **não traz mais o cliente**. O filtro por cliente continua disponível na janela.
- Não exige mudanças no servidor (não precisa rodar o schema.sql de novo além do exigido pela versão 2026-11-04.1).

## 2026-11-04.1
- **Solicitar ordem de produção.** Botão **"📄 Solicitar ordem de produção"** nas telas **Itens por Dia**, **Lista Mestre** e **Plano Mestre**. A janela abre já com os
  filtros da tela (período, recurso, cliente, item, pedido) e permite ajustar: data, recurso, cliente, item (código ou descrição), grupo e pedido. A tabela mostra
  **uma linha por item, com as quantidades somadas** (também linhas, datas, recursos, clientes e litros) e o total geral.
- **Ao gerar, a solicitação é registrada** (número SOLOP-0001, data, hora e usuário) e as linhas do plano ficam **marcadas como solicitadas** ("📄 OP solicitada
  SOLOP-0001"), visível na Lista Mestre e no Plano Mestre; se a quantidade da linha mudar depois, aparece "⚠ qtd. alterada". Por padrão entram só linhas sem Nº OP,
  sem produção e ainda não solicitadas (dá para incluir todas). Há **histórico** das solicitações, **impressão**, **exportação CSV** e **cancelamento**
  (que tira a marca das linhas).
- **Permissão por tela:** campo "Solicitar ordem de produção" na janela de permissões das três telas. Somente leitura não registra.
- **Ação necessária no Supabase:** rodar o arquivo `supabase/schema.sql` de novo no SQL Editor (nova coleção `solicitacoesOP`). Sem isso, as solicitações não
  sincronizam entre os usuários.
- Limite conhecido: gerar o plano automaticamente de novo recalcula as linhas e **remove a marca** das linhas recalculadas (a solicitação continua no histórico).

## 2026-10-31.4
- **Vínculo dos pedidos ajustado automaticamente ao editar quantidades.** Ao alterar a quantidade de uma linha (Lista Mestre ou Plano Mestre), os pedidos em
  aberto do item são **redistribuídos entre as linhas**, do pedido **mais antigo para o mais novo** (menor data de entrega primeiro; empate: menor número
  do pedido), preenchendo cada linha na quantidade informada. Número do pedido, lotes e data de entrega das linhas acompanham. Linhas com produção apontada
  mantêm os seus vínculos. Se as linhas somarem mais que os pedidos em aberto, o excedente fica no pedido mais novo.
- **Não planejar acima do que está em aberto em cada pedido.** Planejar, adicionar linha ou editar a quantidade que deixe o item planejado acima do total em aberto
  dos pedidos passa a ser **bloqueado**, com aviso. Só **administrador** ou o usuário com a nova permissão **"Pode planejar quantidade acima do pedido em aberto"**
  (marcada em Usuários e Permissões → Permissões) pode ultrapassar. Reduzir um excedente que já existe continua permitido.
- A nova permissão fica no perfil do usuário e **não exige rodar o schema.sql** de novo.

## 2026-10-31.3
- **Agrupar por volume (corrige a versão 2026-10-31.2).** Na 2026-10-31.2, ao planejar um pedido, adicionar linha ou reprogramar pendência, a ferramenta
  deixou de somar em linhas existentes e passou a olhar só o pedido (dividia apenas quando o pedido passava do lote máximo). Agora o padrão volta a
  ser **olhar só o volume do item, ignorando o pedido**: completa linhas existentes do mesmo item, data e recurso até o lote máximo e só então abre
  linha nova, dividida pelo lote máximo.
- **Linhas editadas ficam como você definiu.** Linha cuja quantidade você alterou (Lista Mestre ou Plano Mestre) **não é mais completada** pelo agrupamento,
  mesmo menor que o lote máximo. Assim dá para reduzir uma linha e adicionar o restante sem que ele seja somado de volta.
- **Caixa "Agrupar por volume"** na Montagem manual e em "+ Adicionar linha direto aqui" (a escolha é lembrada neste navegador). Desmarcada, cada linha
  adicionada fica exatamente como definida. A geração automática do plano sempre agrupa pelo lote máximo.

## 2026-10-31.2
- **Edições de linhas livres (Lista Mestre e Montagem manual).** Ao **planejar um pedido, adicionar linha ou reprogramar pendência**, a ferramenta
  deixa de somar o pedido em linhas que já existem do mesmo item, data e recurso. Antes, ao reduzir uma linha (ex.: de 1.080 para 500) e adicionar
  o restante, ele era somado de volta na linha reduzida. Agora cada linha fica **exatamente como você a definiu**, inclusive em lotes menores que o
  lote máximo. Continuam como antes: a **geração automática** do plano (agrupa e divide pelo lote máximo), a divisão de uma quantidade **acima**
  do lote máximo ao adicionar, e o bloqueio de editar a quantidade de uma linha para acima do lote máximo.
- **Planejamento de Materiais — colunas de datas mais claras:** "Precisa chegar até" (quando o saldo cruza o estoque de segurança), "Emitir pedido até"
  (essa data menos o prazo de entrega; antes "Comprar até") e "Chega em (se pedir hoje)" (hoje mais o prazo). Os rótulos de situação passaram a
  "Emitir pedido já" e "Emitir pedido até a data".

## 2026-10-31.1
- **Nova tela: Planejamento de Materiais** (menu Planejamento). Projeta, dia a dia, o estoque de cada insumo a partir do plano de produção,
  das entregas programadas e do estoque de segurança, com alerta de falta, data limite para comprar e reposição sugerida. Atualiza sozinha
  quando o plano muda (inclusive por alteração de outro usuário). Considera só o que **ainda falta produzir** (o ERP já baixou o resto) e
  linhas atrasadas consomem a partir de hoje. Prazo em dias corridos; reposição = cobrir as faltas e repor o estoque de segurança.
- **Três importações novas** (Importação de Dados): Pedidos de Compra em Aberto (a lista é substituída a cada importação), Estoque de Segurança e
  Prazo de Entrega por item, e Grupos de Reposição (vários códigos analisados somados, como os aditivos). Cada uma tem permissão própria por usuário.
- **Importação de datas:** data que não existe no calendário (ex.: 31/31/2027) ou texto que não é data agora é recusada com mensagem clara
  (antes era aceita e gravava lixo).
- **Códigos com maiúsculas e minúsculas misturadas** (comum no cadastro do ERP) são reconhecidos como o mesmo item no cálculo de materiais.
- **Sincronização:** receitas sem identificador (por exemplo, de um backup antigo) passam a sincronizar entre usuários (chave = produto + insumo).
- **Ação necessária no Supabase:** rodar o arquivo `supabase/schema.sql` de novo no SQL Editor (há três coleções novas). Sem isso, os dados da tela
  de materiais não sincronizam entre os usuários.
- Arquivos de importação gerados do estudo de estoque de segurança: ver `importacao_materiais/`.

## 2026-10-30.3
- **Importação: número de pedido e quantidade inválidos agora são recusados.** Antes, um valor com texto (ex.: `PED-9001`) virava pedido
  **sem número** ("Pedido undefined") e a linha era aceita. Agora a linha é recusada com a mensagem "o valor "PED-9001" não é um número".
- **Modelos de importação corrigidos:** o modelo de pedidos trazia `PED-5010` de exemplo (formato inválido). Passou a trazer números.
  Se você importou pedidos com o modelo antigo, confira em Cadastros → Carteira de Pedidos se há linhas sem número de pedido.
- **Primeira carga de dados:** a pergunta "Enviar esses dados ao servidor?" ficava escondida atrás da tela "Carregando…". Corrigido; a
  pergunta também passou a usar nomes em português (itens, receitas, recursos, pedidos).
## 2026-10-30.2
- Correção intermediária da pergunta de primeira carga (incluída na 2026-10-30.3).

## 2026-10-30.1
- **Lista Mestre — Lote(s) editável.** A coluna deixou de ser só texto: dá para **trocar** o lote da linha, informar **vários**
  (separados por vírgula ou ponto e vírgula) ou **apagar** (a linha fica sem lote). O lote do pedido não é alterado; o botão **↺**
  volta ao lote do pedido. O lote editado aparece também na Visão do Dia e na impressão, sobrevive à regeneração do plano e é
  sincronizado entre os usuários. Fica registrado no histórico da linha (com o plano confirmado ou em linha com produção).
- **Permissão por usuário** para o Lote: em *Usuários e Permissões → Permissões → Lista Mestre*, o campo **"Lote(s) da linha"** pode
  ser liberado ou travado individualmente (junto dos demais campos da tela).
- **Refugos — filtros separados.** "Código do item" e "Descrição do item" passam a ser dois filtros, ambos digitáveis e de
  **múltipla seleção**; combinam entre si. A trava de item por usuário continua valendo (a descrição só oferece itens permitidos).

## 2026-10-29.3
- Página `configurar.html` (gera o `config.js` testando o servidor); recusa de URL/chave de exemplo e da chave `service_role`.
## 2026-10-29.2
- Página `diagnostico.html`; versão nas telas de entrada e erro; "Detalhes técnicos" na tela de erro.
## Anteriores
- Modo online (Supabase), tempo real com atualização de reserva, biblioteca do Supabase embutida, trava de linhas com produção,
  Pedidos & Lead Time, travas de filtro por usuário e demais funções.
