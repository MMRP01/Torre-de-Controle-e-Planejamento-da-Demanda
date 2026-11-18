# Histórico de versões

A versão aparece no rodapé da tela de entrada ("versão AAAA-MM-DD.N") e no relatório do `diagnostico.html`.
Para atualizar a ferramenta publicada sem perder dados, veja "Atualizar a ferramenta depois" em `CONFIGURAR_SUPABASE.md`.

## 2026-11-13.7
- **Corrigido: barras de busca repetidas em tabelas recriadas pela tela.** Em telas que redesenham a tabela dentro da mesma moldura (como o "Resumo por recurso" da Lista Mestre), a barra de busca do filtro ficava para trás a cada atualização e se empilhava (várias barras iguais acima da tabela). Agora fica sempre uma só.
- **Tabelas de resumo sem filtro:** "Resumo por recurso" (Lista Mestre) e "Por terceiro" (Terceirização) deixam de ter a barra de busca e os ▾, pois são resumos curtos. (Qualquer tabela pode ser excluída com data-xf="off".) Sem mudança no servidor.

## 2026-11-13.6
- **Itens por Dia: só os itens com planejamento no período.** Ao filtrar os dias, a matriz mostra apenas os itens com algo planejado nesses dias (e os atrasados cuja nova data prevista cai no período). Nova caixa "Só itens com planejamento no período" (marcada por padrão; desmarcar mostra todos os itens com pedido em aberto;
  "Limpar filtros" volta ao padrão). Um aviso diz quantos itens com pedido em aberto ficaram ocultos e quantas unidades faltam programar neles; os cartões do topo e a exportação (.csv) seguem os itens mostrados. Sem mudança no servidor.

## 2026-11-13.5
- **Lista Mestre: filtros de datas de efetivo e de turno.** Novos filtros no topo: Última data efetiva (de/até), Data do turno (de/até) e Turno (1º, 2º, 3º). Somam-se aos demais filtros, valem para os totais e para as ações que usam o filtro da Lista, e "Limpar filtros" os esvazia.
- **Itens por Dia: identificação de atraso e nova data.** O item em atraso ganha etiquetas na descrição ("⏰ Em atraso: N linha(s) · X unid.", "sem nova data: N", "📅 nova data prevista: dd/mm (X unid.)") e marcas nas células dos dias: ⏰ no dia do plano, ⏰! quando não há nova data e 📅 +X no dia da nova data.
  As quantidades da matriz seguem as do plano; legenda na tela.
- **Relatório de datas ajustadas: formato "Matriz por dia".** Nova opção de Formato que mostra o relatório no formato da tela do Itens por Dia, com a quantidade pendente das linhas atrasadas no dia da nova data (o efetuado fica no dia do plano; atraso sem nova data fica na data do plano), com filtro de dias (padrão hoje +13, máximo 90),
  cliente, busca e "Só itens com atraso ajustado". CSV, Excel e PDF saem no mesmo formato. O formato Lista continua como estava. A data do plano não é alterada. Sem mudança no servidor.

## 2026-11-13.4
- **Nova data por atraso (Itens por Dia).** Alerta no topo do Itens por Dia com as linhas em atraso (data do plano anterior a hoje, com quantidade pendente e fora de Concluído), segundo os filtros de cliente, item e recurso da tela.
  O botão **📅 Informar nova data** abre uma janela para informar a nova data de cada linha (hoje ou depois; "aplicar a todas as sem data"; ✕ para tirar). A **data do plano NÃO muda** (o Planejado x Efetuado segue igual): a nova data é gravada na linha com o motivo "Atraso", quem informou e quando,
  e aparece no relatório de atualizações. Alerta de "nova data vencida". Botão **📄 Relatório de datas ajustadas**: lista as datas informadas (cliente, item, pedido, pendente, data do plano, nova data, atraso informado, motivo, situação), com filtros e saídas em CSV, Excel e PDF.
  Permissão por campo "Informar nova data de produção (atraso)" em Itens por Dia (o relatório abre para quem vê a tela). Sem mudança no servidor. Documentação: IT-PCP-025 nova.

## 2026-11-13.3
- **Filtro independente em cada coluna, com vários itens.** Volta o ▾ no título de cada coluna (discreto; vermelho quando há filtro), que abre a lista de valores DAQUELA coluna: marcar um ou mais itens, pesquisar, ordenar e filtrar por condição de texto, número ou data.
  Colunas diferentes se somam (marcar vários itens em várias colunas ao mesmo tempo). Mantidos da versão anterior: a barra enxuta com a busca em todas as colunas, as etiquetas dos filtros ativos, "limpar tudo", ordenar clicando no título e a ordem original ao tirar a ordenação.
  Sai o botão "Filtros" com painel único e seletor de coluna. Os ▾ e a barra só aparecem em tabelas com 6 linhas ou mais (ou com filtro ativo). Na Lista Mestre, a linha de filtros que mudam os totais continua escondida (atalho "filtros que mudam os totais" na barra). Sem mudança no servidor.

## 2026-11-13.2
- **Filtro das tabelas simplificado: uma barra única por tabela.** Saem os botões ▾ de cada coluna. Acima de cada tabela com 6 linhas ou mais (e de qualquer tabela com filtro ativo) fica uma barra enxuta: caixa **Buscar em todas as colunas** (várias palavras, sem diferenciar
  acento nem maiúscula) e botão **⚙ Filtros**, que abre UM painel com seletor de coluna (ordenar, condições de texto, número e data, pesquisa e valores marcáveis). Os filtros ativos viram etiquetas na barra (clique para editar, ✕ para tirar) e há "✕ limpar tudo".
  Clicar no título da coluna ordena (▴ ▾; o terceiro clique volta à ordem original). Na Lista Mestre, a linha de filtros por coluna (que também muda os totais) fica escondida e aparece sozinha quando há filtro dela ativo, ou pelo atalho "filtros por coluna (totais)".
  Corrigidos: voltar à ordem original ao tirar a ordenação e o texto digitado na busca que podia ser apagado por um redesenho. Sem mudança no servidor.

## 2026-11-13.1
- **Relatório de reposição usa os cenários de "em processo" por material da tela.** Ao abrir o relatório, a caixa "Usar os N cenário(s) por material da tela" vem marcada: o relatório mostra os mesmos números da tela, registra quais cenários usou (cabeçalho, seção Avisos e Parâmetros do Excel e do PDF) e o botão geral no momento.
  Desmarcar a caixa gera só com o botão geral. Sem cenários na tela, a caixa não aparece. Relatórios antigos continuam abrindo. O cenário continua não sendo gravado nos dados e o Planejamento de Materiais segue só o botão geral. Sem mudança no servidor.

## 2026-11-12.9
- **Permissão "Alterar linhas com produção apontada".** Nova caixa na tela de permissões do usuário (por padrão só administradores): quem a recebe altera data, recurso, quantidade e exclusão das linhas com produção apontada na Lista Mestre e no Plano Mestre, sempre com justificativa
  registrada com o nome de quem alterou. Também vale no servidor: **rodar o schema.sql de novo** (função pode_alterar_apontadas e coleção do histórico de atualizações).
- **Plano de Reposição: "Considerar em processo" por material.** Cada item e grupo tem a sua caixa (grade, lista de ações e detalhe) para analisar o cenário dele, com o selo "cenário" e "↺ limpar cenários". Só na tela e na sessão; o relatório de reposição segue o botão geral.
- **Terceirização.** Coluna "Terceiro" na Lista Mestre (linha a linha ou em lote nas linhas filtradas). A linha terceirizada mantém data, quantidade, OP e apontamento, mas sai dos indicadores de produção (Dashboards, Planejado x Efetuado), da Capacidade, da capacidade usada no
  Plano Mestre e da alocação na geração do plano; o consumo de insumos continua entrando. Nova tela "Terceirização" (cartões, resumo por terceiro, linhas com status, filtros e CSV). As marcas voltam nas linhas novas do mesmo item e pedido ao refazer o plano.
- **Filtro estilo Excel em todas as tabelas** (telas e janelas de relatório): ordenar, pesquisa na lista, valores marcáveis com contagem, condições de texto, número e data, filtros encadeados, barra com o total filtrado; continua ao redesenhar a tabela.
- **Relatório de atualizações por tela** (botão 🕒 Atualizações em cada tela e link "ver o que mudou" em Itens por Dia): o que mudou, quem, quando, tela, campo e valores antes e depois; resumo único para ações em lote; 90 dias / 5.000 lançamentos; vale a partir da ativação.
- Documentação: IT-PCP-023 (terceirização) e IT-PCP-024 (relatório de atualizações) novas; POP e ITs 001, 004, 007, 009, 013, 014, 015, 016 e 017 atualizados.

## 2026-11-12.8
- **Grupos de reposição montados pelo Subgrupo do cadastro de itens.** Itens com o mesmo **Subgrupo** (2 ou mais) passam a ser planejados como um só material (estoque, consumo, entregas, estoque de segurança, máximo e prazo
  somados), sem precisar importar o arquivo "Grupos de reposição". "Sem subgrupo" e subgrupos com um item só continuam individuais; um grupo **importado** sempre vale mais (seus itens saem do grupo automático).
  Parâmetros do grupo: estoque de segurança e máximo = **soma** dos itens; prazo = **maior** prazo dos itens (parâmetros importados por item). Podem ser **ajustados** (a sugestão de estoque de segurança grava o valor no
  grupo, sem mexer nos itens). A lista de itens do grupo é sempre recalculada do cadastro. Vale no Plano de Reposição, no Planejamento de Materiais, no relatório de reposição e na sugestão de estoque de segurança.
  Painel "Grupos pelo Subgrupo" no cartão Grupos de reposição (Importação de Dados), com a chave para ligar e desligar (permissão própria; sincronizada; padrão ligado). Sem mudança no servidor.

## 2026-11-12.7
- **Relatório de reposição: cada linha tem a sua caixa de incluir/tirar.** Antes a caixa agia sobre o material inteiro, então desmarcar uma linha tirava todas as linhas do mesmo item. Agora só a linha desmarcada sai
  (as outras linhas do mesmo material continuam); o material só sai da grade de saldos quando todas as linhas dele foram tiradas. O rodapé e o registro dizem "linha(s) tirada(s)" (o Excel traz "Linhas tiradas do relatório").
  A rolagem da tabela é preservada ao marcar e desmarcar. A simulação da quantidade a pedir não muda por tirar uma linha do relatório.
- **Relatório de reposição: layout de impressão (PDF) enxuto.** A lista impressa traz só: Data da ação, Ação, Código, Descrição, UM, Quantidade, Chegada necessária, Quantidade sugerida e Simulação com a quantidade pedida.
  O relatório na ferramenta (prévia e resultado), o Excel e o CSV continuam com todas as colunas. Sem mudança no servidor nem nos dados.

## 2026-11-12.6
- **Relatório de reposição e lista do Plano de Reposição: o filtro "Ação do plano" passa a valer por linha.** Antes só filtrava o material pela ação principal; como o alerta de excesso é independente dela, um material que
  precisava comprar também mostrava linhas de "Reduzir / adiar entrega" ou "Não comprar" mesmo com esses tipos desmarcados. Agora cada linha só entra se o tipo dela foi escolhido (e o material entra se a ação principal ou
  alguma linha dele foi escolhida); "Emitir pedido hoje" e "até a data" separam os pedidos pela data de emissão. Vários grupos escolhidos na tela também passam a ser respeitados no relatório ("Grupos escolhidos na tela", com "✕ remover").
- **Quantidade a pedir editável no relatório de reposição, com simulação.** Antes de gerar, cada linha de compra tem um campo com a quantidade sugerida, editável; a coluna **Simulação** refaz o saldo do material com a chegada
  dessa quantidade e sinaliza: Atende, Abaixo do segurança, Ainda falta (com a data) ou Passa do máximo, e um resumo sob os indicadores conta os materiais em cada situação. A atualização é feita no lugar (mantém o foco e a rolagem).
  As quantidades editadas ficam no relatório gerado (com a sugerida e a simulação, também no Excel, PDF e CSV) e **não entram em nenhum cálculo** do Plano de Reposição: serão lançadas depois em Pedidos de compra em aberto.
  A simulação reproduz o saldo com plano do motor (conferido nos materiais com compra). Relatórios gravados antes desta versão continuam abrindo e exportando. Sem mudança no servidor nem nos dados.

## 2026-11-12.5
- **Sugestão de estoque de segurança: média mensal (D) e metade da média mensal (E).** D = consumo total ÷ (dias do período ÷ dias do mês, padrão 30), com os mesmos filtros dos outros métodos (período, planejado ou efetuado,
  componentes, grupos) e o mesmo valor nas duas bases da média; E = metade de D. Entram na tabela, no Excel/CSV, no registro das aplicações (ESEG) e nas opções de escolha: "Usar em todos os materiais mostrados" e "Usar" por material.
  A janela avisa quando o período tem menos de um mês (D e E viram projeção). Agora são cinco métodos lado a lado (A a E). Sem mudança no servidor nem nos dados.

## 2026-11-12.4
- **Sugestão de estoque de segurança: média por dia calculada sobre "todos os dias do período" (padrão) ou "só os dias com consumo".** Na segunda opção a média é o consumo total ÷ os dias em que houve consumo (média por dia de consumo)
  e a cobertura passa a contar **dias de consumo**: o método A cobre N dias de consumo (padrão 2), o B usa os consumos esperados dentro do prazo × fator + folga em dias de consumo (padrão 0); o C não muda.
  Os parâmetros voltam aos padrões da base escolhida ao trocar; as colunas, o Excel/CSV (ambas as médias e a média usada) e o registro das aplicações (ESEG) guardam a base. Sem mudança no servidor nem nos dados.

## 2026-11-12.3
- **Setas de rolar para o lado nos cantos da tabela.** Na versão anterior a seta esquerda ficava logo depois das colunas fixas e, com Data e Item largos, caía no meio da tabela, sobre os campos. Agora a esquerda fica no
  canto esquerdo da área da tabela e a direita no canto direito, no meio da parte visível, em qualquer largura de janela e com ou sem menu recolhido. Sem mudança no servidor nem nos dados.

## 2026-11-12.2
- **Setas de rolar para o lado (‹ ›) acompanham a tabela e a tela.** Antes eram fixas na janela (esquerda a 252 px, meio da janela): com o menu recolhido, a esquerda ficava no meio do conteúdo. Agora a esquerda fica logo
  depois das colunas fixas, a direita na borda da tabela, as duas no meio da parte VISÍVEL da tabela, e somem quando a tabela está fora da tela, quando não há o que rolar ou ao chegar ao fim daquele lado.
  Reposicionam ao rolar a página ou a tabela, redimensionar, recolher o menu e mudar as colunas fixas. (Lista Mestre, Itens por Dia e Planejado x Efetuado.)
- **Colunas fixas:** nova opção **"Código e descrição"** (fixa também a descrição, mesmo em tela pequena). "Só o código" passa a fixar as colunas de código (na Lista Mestre: Data e Item, e não só a Data).
- Sem mudança no servidor nem nos dados.

## 2026-11-12.1
- **Telas menores: as tabelas voltam a aparecer.** Em notebook e janela pequena, as colunas congeladas ocupavam quase toda a área (Necessidades deixava 19% da área livre a 1280 px; Itens por Dia, 32%).
  Agora: (1) as colunas de **descrição congeladas têm largura limitada** (240 px, quebram em mais linhas; o texto inteiro vai no balão); (2) o **congelamento é adaptativo**: só ficam fixas as colunas que cabem em ~42% da
  área visível; (3) o **menu lateral recolhe sozinho abaixo de 1400 px** (gaveta com ☰; o botão do menu guarda a escolha neste navegador); (4) cada tabela larga tem a chave **❄ Colunas fixas** (Automático, Só o código ou Nenhuma),
  lembrada por navegador. A 1280 px a área livre vai a 70–78% nessas telas. Quem só lê também pode usar a chave e o botão do menu (são preferências de tela).
- **Correção nas matrizes de cabeçalho duplo (Itens por Dia e Planejado x Efetuado):** as células Qtd./Litros do cabeçalho eram marcadas como fixas por engano e as larguras eram medidas na linha errada.
  O congelamento agora usa o mapa real das colunas (rowSpan/colSpan) e mede pela primeira linha de dados.
- Sem mudança no servidor nem nos dados.

## 2026-11-11.1
- **Estoque por depósito (Estoque e Em processo).** A importação de estoque reconhece o relatório do ERP com **uma coluna por depósito**: cada depósito é classificado como **Estoque**, **Em processo** ou
  **Ignorar** (classificação pré-carregada e editável no painel "Depósitos", no cartão de Estoque; mudar a classificação recalcula os saldos sem reimportar). O saldo por depósito fica guardado no item. Itens
  fora do cadastro são ignorados com um aviso (não viram erro) e depósito novo entra como Ignorar até ser classificado. A planilha simples (Código; Estoque Atual) continua valendo e aceita a coluna Em Processo.
- **Duas colunas "Estoque" e "Em processo"** no Cadastro de Itens, Necessidades, Necessidades por Grupo, Planejamento de Materiais, grade do Plano de Reposição e relatório de compras, e a opção
  **"Considerar o estoque em processo nos cálculos"** (global, sincronizada, desligada por padrão). A geração do plano continua usando só o Estoque.
- **Sugestão de estoque de segurança a partir das OPs do ERP**, por item e por grupo de reposição, com **três métodos lado a lado** (A cobertura fixa, B cobertura pelo prazo de entrega, C estatístico), comparação
  com o valor atual, alertas (histórico curto, sem prazo), escolha por material, aplicação com **registro (ESEG-nnnn) do antes e depois**, histórico e saídas em Excel e CSV. Botão na tela de Planejamento de Materiais.
- **Plano de Reposição: filtro por legenda** (Não atende, Atende mas abaixo do estoque de segurança, Atende, Acima do estoque máximo), também no relatório de reposição.
- **Itens por Dia: "Última atualização dos dados"** (data, hora e usuário) e a última importação de pedidos.
- **Lista Mestre:** o selo "alterada" passou para baixo do campo de data (não cobre mais o Recurso).
- **Servidor:** coleção nova `aplicacoesSeguranca`: é preciso rodar o **supabase/schema.sql** de novo (além da coluna da visão por usuário, da versão anterior).

## 2026-11-10.1
- **Visão por usuário: o administrador escolhe o que cada pessoa enxerga.** Na janela de permissões do usuário há a seção **"O que este usuário enxerga"**, com tudo marcado (visível) por padrão:
  - **Colunas de todas as tabelas** (34 tabelas, 250 colunas; as colunas de dias contam como um grupo). Valem na tela, na impressão da Lista Mestre e nos CSV da Lista Mestre, de Refugo e do
    Histórico de importações; nas demais exportações, esconda também o botão de exportar.
  - **Selos**, por família (19 famílias mais "Demais selos").
  - **Comentários das linhas**: o botão Obs., a linha amarela e a observação impressa; quem não vê também não abre, não grava nem apaga a observação.
  - **Botões de ação**, por tela (Gerar plano, Solicitar OP, Relatórios, Importar, Backup, Exportar CSV, cadastros e outros). Um botão escondido também fica **bloqueado**.
  Administradores veem tudo. **É uma restrição visual** (as permissões são aplicadas no navegador): organiza a tela de cada perfil, mas não protege informação sigilosa. As alterações ficam no registro de acessos.
- 5 tabelas ganharam identificação (Localizações de granel, Resumo da Lista Mestre e os três quadros dos Dashboards).
- **Coluna nova no servidor (perfis.visao): é preciso rodar o supabase/schema.sql de novo** (ele acrescenta a coluna sem apagar nada).

## 2026-11-09.1
- **Capacidade dos Recursos: resumo ao clicar na célula.** Clicar numa célula (recurso x dia) abre o resumo dos **itens e quantidades alocados** naquele dia: capacidade base, paradas descontadas,
  capacidade do dia, alocado, ocupação e saldo; tabela por item (quantidade, litros, % da capacidade, linhas, Nº OP, Nº OP Granel, pedidos, clientes e situação); paradas do dia; e o botão
  "Abrir na Lista Mestre" (filtra o dia e o recurso). Quem só consulta também abre.
- **Lista Mestre: data de produção editável**, com a mesma regra do Plano Mestre (plano confirmado exige justificativa e grava o histórico da linha; linha com produção apontada só administrador altera).
  Nova permissão **"Data de produção da linha"** na Lista Mestre.
- **Histórico de importação: detalhe do Resultado.** O selo de Resultado abre o resumo dos erros e avisos com **item/referência, motivo e ação para correção**, e exporta em **Excel** (Resumo, Erros e avisos,
  Por motivo) e CSV. Cada importação guarda até 300 erros; **só as 50 importações mais recentes mantêm o detalhe** (as antigas ficam só com as contagens).
- **Todos os selos clicáveis.** Ao clicar em qualquer selo da ferramenta abre um resumo: o que é, números, itens, relatórios e registros ligados (com botão Abrir) e ação sugerida. As famílias conhecidas
  (solicitação de OP, status, contaminação, paradas, usuários, grupos, materiais, reposição, insumos, importação, Lead Time e outras) têm explicação própria; os demais selos recebem uma explicação pela cor
  e pelo contexto da linha. Selos que já têm ação própria e selos dentro de botões ou links mantêm o comportamento anterior.
- Não há coleção nova no servidor: **não é preciso rodar o schema.sql de novo** por causa desta versão.

## 2026-11-08.1
- **Registro das importações (data, hora e usuário).** Cada importação em *Importação de Dados* passa a gravar **quando** foi feita (data e hora), **quem** executou (usuário e nome),
  qual importação, o modo (Atualizar ou Substituir), o **arquivo**, as linhas lidas, os adicionados, os atualizados, os erros e o resultado (Importado, Importado com erros, Nada
  importado ou Falha ao ler o arquivo). Vale para as 9 importações (Itens, Receitas, Pedidos, Estoque, Pedidos de compra, Estoque de segurança e prazo, Ordens de Produção do ERP,
  Grupos de reposição e Prioridades). Cada cartão mostra a **"Última importação"** (data, hora, usuário, arquivo e contagens), e há um **"Histórico de importações"** no alto da tela,
  com filtros por importação e por usuário e exportação em CSV. O registro **não pode ser apagado pela tela**, é compartilhado entre os usuários e guarda as últimas 1000.
- **Coleção nova no servidor** (historicoImportacoes): é preciso rodar o **supabase/schema.sql** de novo.

## 2026-11-06.2
- **Relatório de insumos — escolha das seções.** Antes de gerar, a janela tem **"Incluir no relatório"**: Resumo por insumo, Por OP e granel, Granel consumido e Pendências. Só o
  que ficar marcado entra no **Excel** (uma aba por seção, mais os Parâmetros), no **PDF** e no **CSV** (que leva o resumo, então fica desabilitado sem ele). As abas das seções
  desmarcadas ficam esmaecidas na prévia. A escolha é lembrada neste navegador, vale a regra de marcar ao menos uma seção, e o histórico mostra as seções de cada relatório.
- **Relatório de reposição** (botão **📄 Relatório de reposição** no Plano de Reposição). Lista das reposições (compra emergencial, pedidos a emitir, reduzir/adiar entrega, não
  comprar) pelos filtros da janela (**ação do plano, tipo, grupo, material, pedidos atrasados, horizonte e ciclo**), que partem dos da tela. A lista é **a mesma da tela** para os
  mesmos filtros. Tem prévia com indicadores, **escolha das seções** (Lista de reposição, Grade de saldos por dia, Avisos), caixa para **excluir materiais** antes de gerar,
  **registro** (RREP-0001, usuário, data, filtros), histórico e exportação em **Excel**, **PDF** (impressão em paisagem) e **CSV**. A grade de saldos por dia só fica disponível logo
  depois de gerar; o histórico guarda a lista e os avisos.
- Nova permissão **"Relatório de reposição"** (Plano de Reposição). **Coleção nova no servidor** (relatoriosReposicao): é preciso rodar o **supabase/schema.sql** de novo.

## 2026-11-06.1
- **Relatório de insumos** (botão **📊 Relatório de insumos** na Lista Mestre). Resumo dos insumos a consumir nas linhas dentro dos filtros (data, recurso, cliente, item, grupo,
  pedido, "só sem produção apontada"), **antes de gerar**: janela com prévia, indicadores, abas (Resumo por insumo, Por OP e granel, Granel consumido, Pendências, Linhas) e caixa
  para **excluir linhas**. Ao gerar, o relatório é **registrado** (RINS-0001, usuário, data, filtros) e pode ser exportado em **Excel** (uma aba por bloco), **PDF** (pela impressão
  do navegador) e **CSV**; há histórico. O consumo vem das **OPs do ERP**: o **Nº OP** (envase) e o **Nº OP Granel** (mistura) de cada linha; **cada OP é contada uma vez**, mesmo
  que apareça em várias linhas. O Nº OP Granel pode ter **vários números** (separados por vírgula, ponto e vírgula, barra, + ou "e"). Quando falta OP (não digitada ou fora da
  importação), a parte que falta é **estimada pela receita** e marcada como estimada. Vale a **quantidade da OP do ERP**, com aviso quando a Lista Mestre diverge (tolerância de 1%).
  Só entram como insumo os componentes **INS-…**; recursos e mão de obra são ignorados; o granel consumido aparece à parte; códigos suspeitos (ex.: RNS-OB-…) são avisados.
- **Importação "Ordens de Produção do ERP (componentes)"** (Importação de Dados): lê o relatório do ERP (Nº DA OP, item, quantidades, componentes), uma OP por registro; atualizar
  substitui só as OPs que vierem no arquivo; "substituir" troca toda a base de OPs. Normaliza códigos em minúsculas.
- Nova permissão **"Relatório de insumos"** (Lista Mestre). **Duas coleções novas no servidor** (ordensERP e relatoriosInsumos): é preciso rodar o **supabase/schema.sql** de novo.

## 2026-11-05.5
- **Plano de Reposição** (ajuste recebido, aplicado sobre esta versão). Nova tela no menu **Planejamento**: mostra o **saldo diário de cada material** (estoque + entregas −
  consumo do plano) comparado ao **estoque de segurança** e ao **estoque máximo**, e o que comprar, quanto e para quando. Traz indicadores (compra emergencial / antecipar,
  pedidos a emitir, entregas que geram excesso, acima do máximo), filtros (ação do plano, tipo, grupo, material, pedidos de compra atrasados, horizonte e ciclo de reposição),
  a **grade de saldos por dia** colorida (atende, abaixo do segurança, falta, excesso, entrega programada) e a **lista de ações** (comprar / antecipar), com exportação em CSV.
- **Estoque Máximo** nas importações do Planejamento de Materiais: os cartões "Estoque de Segurança e Prazo de Entrega" e "Grupos de Reposição" ganharam a coluna opcional
  "Estoque Máximo" (célula em branco não apaga o valor existente). Sem estoque máximo, o nível alvo dos pedidos é estimado (segurança + consumo médio × (prazo + ciclo)).
- A tela de permissões passa a listar o Plano de Reposição (16 telas operacionais). Não exige mudança no servidor.

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
