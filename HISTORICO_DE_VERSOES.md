# Histórico de versões

A versão aparece no rodapé da tela de entrada ("versão AAAA-MM-DD.N") e no relatório do `diagnostico.html`.
Para atualizar a ferramenta publicada sem perder dados, veja "Atualizar a ferramenta depois" em `CONFIGURAR_SUPABASE.md`.

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
