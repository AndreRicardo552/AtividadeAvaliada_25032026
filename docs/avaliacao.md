# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: André Ricardo Monteiro da Rocha
RA: 24001777
Data: 25/03/2026  

---

# 1. Definição do MVP
Descreva aqui **qual parte do sistema** foi incluída no seu MVP.  
Explique claramente:

O que está dentro:
    Busca abranger todo o processo de venda e estoque, para tornar o produto viável comercialmente sem necessitar de funções extremamente complexas. Garantindo a capacidade de operar uma venda, mesmo em medicamentos controlados logo no MVP, assim como não impedir vendas a prazo para conveniados.

O que está de fora:
    Controle do contas a pagar, o MVP carece de ferramentas avançadas para controlar, monitorar e validar o contas a pagar de toda a matriz. Também ficou de fora a geração de relatórios e dashboards avançados para BI (Business Intelligence).

Por quê?:
    O MVP foi planejado para ter controle total das vendas, permitindo a operação com um processo mínimo de entrada de notas, porém com validação forte das vendas. Gerando assim lucratividade para o cliente logo no começo do projeto e focando na segurança da transação, no controle do estoque e na manutenção básica de usuários e clientes.

---

# 2. Regras de Negócio (mínimo: 5)
Liste e descreva **cada RN** de forma clara.

RN01 - Validação do produto na venda - O sistema não pode permitir venda de estoque zerado ou negativo e venda de produto inexistete.
RN02 - Bloqueio por receita - Não é possivel vender produtos que precisam de receita sem a apresentação de uma valida.
RN03 - Validação de cadastro - Não é possivel cadastrar um produto sem incluir as caracteriscas de venda e associar a um fornecedor.  
RN04 - Restrição de venda a prazo - Vendas a prazo só podem ser realizadas para clientes conveniados ou com cadastro recorrente aprovado.
RN05 - Estoque individual por loja - O estoque deve ser contado por loja, idependente de modelo de DB unico ou separado.   
RN06 - Registro de ações financeiras - Toda operação financeira deve ser associada ao contas a pagar ou receber(dependendo do tipo de operação).
RN07 - Registro de logs - Toda operação que gera ação no sistema deve ser registrada em logs para criação de relatorios e auditoria.
RN08 - Perfil de usuario - O Sistema deve ser guarnecido de controle de perfil de usuarios no modelo RBAC.
RN09 - Venda controlada deve ter validação de receita por usuario habilitado.

---

# 3. Requisitos Funcionais (mínimo: 8)
Liste os requisitos funcionais do seu MVP.

RF01 —  O sistema deve permitir vendas no PDV
RF02 —  O sistema deve permitir o cadastro de usuarios e hierarquias
RF03 —  O sistema deve permitir o cadastro de produtos
RF04 —  O sistema deve permitir entrada de nota fiscal
RF05 —  O sistema deve permitir Visualizar relatorios
RF06 —  O sistema deve emitir alerta de estoque minimo
RF07 —  O sistema deve permitir venda a prazo a conveniados
RF08 —  O sistema deve permitir o cadastro de clientes
RF09 —  O sistema deve Emitir cupom fiscal
---

# 🛡 4. Requisitos Não Funcionais (mínimo: 4)
Liste os RNFs do sistema conforme seu MVP.

RNF01 — O sistema deve ser seguro, implementando criptografia de dados sensíveis e controle de acesso RBAC.
RNF02 — A interface deve ser aprimorada, ajudando o usuario a manuzear as ferramentas, inclusive atalhos de pdv.
RNF03 — O sistema deve ter disponibilidade offline, incluindo funcionamento idependente do PDV para evitar bloqueio de vendas.
RNF04 — O sistema deve ter auditoria, registrar logs em todas as ações.


---

# 5. Casos de Uso (mínimo: 10)
### Inserir **diagrama de casos de uso geral**, demonstrando claramente:
- os 10 casos
- relação entre eles e atores
- pelo menos 3 includes
- pelo menos 3 extends

UC01 - Realizar Venda (Atendente)
UC02 - Identificar Cliente (Atendente)
UC03 - Consultar Produto (Atendente)
UC04 - Verificar Estoque (Sistema)
UC05 - Finalizar Operação (Atendente / Sistema)
UC06 - Realizar Venda a Prazo (Atendente)
UC07 - Receber Compra de Fornecedor (Gerente)
UC08 - Atualizar Estoque (Sistema)
UC09 - Validar Receita (Farmacêutico)
UC10 - Cadastrar Produto (Gerente)
---

# 6. Documentação dos Casos de Uso
Para **cada caso de uso**, utilize o template abaixo:
---

## **UC01 — Realizar Venda**
**Ator(es):** Atendente  
**Descrição:** Processo de registrar os produtos que o cliente deseja comprar no caixa.  
**Pré-condições:** O sistema do caixa precisa estar aberto e os produtos cadastrados.  
**Pós-condições:** O cliente leva os produtos, e o valor da compra é registrado.

### Fluxo Principal
1. O atendente passa os produtos no leitor de código de barras ou digita o código na tela.
2. O sistema verifica as informações do produto, como o preço.
3. O atendente pergunta se o cliente deseja informar o CPF.
4. O sistema busca pelo cliente caso o CPF seja informado.
5. O atendente avança para a tela de pagamento.
6. O sistema confere rapidamente se ainda há o produto na prateleira.
7. Estando tudo certo, a venda é finalizada e o cupom é gerado.

### Fluxos Alternativos / Exceções
- FA01 — O cliente não tem cadastro. O sistema permite fazer um cadastro rápido antes de finalizar.
- FA02 — O produto é de uso controlado. O sistema avisa e pede a autorização do farmacêutico.

### Relacionamentos
- **Include:** UC02 (Identificar Cliente), UC03 (Consultar Produto), UC04 (Verificar Estoque), UC05 (Finalizar Operação).
- **Extend:** UC06 (Realizar Venda a Prazo), UC09 (Validar Receita).

---

## **UC02 — Identificar Cliente**
**Ator(es):** Atendente  
**Descrição:** Momento em que o cliente informa quem ele é durante uma compra, para ganhar descontos ou pontuar.  
**Pré-condições:** A tela de buscar cliente deve estar aberta no caixa.  
**Pós-condições:** A compra fica registrada no nome e CPF desse cliente.  

### Fluxo Principal
1. O atendente pede o CPF ou o nome completo do cliente.
2. O sistema procura os dados desse cliente.
3. O sistema mostra o nome encontrado na tela para confirmação.
4. O atendente confirma com o cliente e junta essa informação à compra atual.

### Fluxos Alternativos / Exceções
- FA01 — Cliente não encontrado. O sistema permite anotar os dados rapidamente para concluir a venda.
- FA02 — Questão de crédito. O sistema avisa se houver alguma restrição no nome e não permite vendas a prazo.

### Relacionamentos
- **Include:** UC02 - Identificar Cliente (Atendente)
- **Extend:** Nenhum. 

---

## **UC03 — Consultar Produto**
**Ator(es):** Atendente  
**Descrição:** Uma pesquisa rápida que o atendente faz para saber o preço ou se tem o produto na loja.  
**Pré-condições:** Ter os produtos da loja cadastrados no computador.  
**Pós-condições:** O atendente vê na tela o preço, nome e quantidade do produto.  

### Fluxo Principal
1. O atendente digita o nome do remédio ou do produto.
2. O sistema procura na lista e mostra as opções encontradas.
3. O atendente confere a marca e a dosagem solicitada pelo cliente.

### Fluxos Alternativos / Exceções
- FA01 — O produto não foi encontrado. O sistema mostra um aviso de que não achou nada com esse nome.
- FA02 — O produto existe, mas está com o preço zerado. O sistema avisa que o valor não foi estipulado.

### Relacionamentos
- **Include:** UC03 - Consultar Produto (Atendente), UC04 - Verificar Estoque (Sistema)
- **Extend:** Nenhum. 

---

## **UC04 — Verificar Estoque**
**Ator(es):** Sistema  
**Descrição:** Uma conferência automática no sistema da loja para ter certeza de que o produto não acabou.  
**Pré-condições:** O atendente deve ter escolhido um produto na tela de vendas.  
**Pós-condições:** O produto é liberado para ser levado pelo cliente no sistema.  

### Fluxo Principal
1. O sistema recebe a informação de qual produto o cliente quer.
2. Ele checa as quantidades que ficam anotadas no computador da loja.
3. Se verificar que ainda há unidades sobrando, ele permite passar o item no caixa.

### Fluxos Alternativos / Exceções
- FA01 — Produto esgotado. O sistema avisa o atendente na hora e não deixa adicionar o item.
- FA02 — Lentidão na verificação. O sistema tenta conferir de novo o estoque após alguns segundos.

### Relacionamentos
- **Include:** UC04 - Verificar Estoque (Sistema)
- **Extend:** Nenhum.

---

## **UC05 — Finalizar Operação**
**Ator(es):** Atendente, Sistema  
**Descrição:** O momento final da compra, onde o cliente escolhe a forma de pagamento e leva a sua notinha.  
**Pré-condições:** Ter produtos selecionados no caixa e, opcionalmente, os dados do cliente informados.  
**Pós-condições:** O dinheiro entra no caixa e a operação conclui com a impressão.

### Fluxo Principal
1. O atendente informa que os produtos encerraram e vai fechar o pedido.
2. O sistema mostra o valor total, descontos e possíveis impostos.
3. O atendente informa se vai ser pago em dinheiro, Pix ou cartão.
4. O sistema fecha a compra, guarda as informações e manda imprimir o cupom.

### Fluxos Alternativos / Exceções
- FA01 — Sem internet ou problema na rede. O sistema guarda a nota para enviar pro governo assim que a conexão voltar.
- FA02 — Cartão de crédito foi recusado. O sistema avisa o erro para o atendente pedir outra forma de pagamento.

### Relacionamentos
- **Include:** UC05 - Finalizar Operação (Sistema)
- **Extend:** Nenhum.

---

## **UC06 — Realizar Venda a Prazo**
**Ator(es):** Atendente  
**Descrição:** Situação onde o cliente pode levar agora e abater de convênios/fiado, pagando no futuro.  
**Pré-condições:** O cliente já precisa ter sido identificado no caixa com um CPF liberado.  
**Pós-condições:** Fica anotado no sistema que existe um valor ainda pendente deste cliente.

### Fluxo Principal
1. O atendente escolhe a opção "Convênio" ou "A Prazo" na hora do fechamento.
2. O sistema avalia se esse cliente pode ter valores a prazo ainda.
3. Estando dentro do limite permitido, o sistema anota a pendência dele ou da empresa parceira e libera os produtos.

### Fluxos Alternativos / Exceções
- FA01 — O cliente tentou comprar acima do que podia. O sistema bloqueia aquele pagamento e pede um dinheiro ou cartão diferente.
- FA02 — Os dados de telefone e endereço estão muito antigos. O atendente pede para o cliente preencher tudo de novo, atualizando para liberar.

### Relacionamentos
- **Include:** UC06 - Realizar Venda a Prazo (Atendente)
- **Extend:** UC01 Para venda a prazo (Convênio).

---

## **UC07 — Receber Compra (Fornecedor)**
**Ator(es):** Gerente  
**Descrição:** Momento em que caminhões entregam produtos novos na loja e o gerente precisa dar a entrada deles no sistema.  
**Pré-condições:** A mercadoria física e a nota do fornecedor devem estar com a gerência.  
**Pós-condições:** Os produtos passam a constar no controle da farmácia prontos para subir pro salão.  

### Fluxo Principal
1. O gerente abre a janela de notas no sistema do escritório.
2. Ele insere a chave da nota que veio em anexo ou carrega o arquivo.
3. O computador faz uma conferência cruzando os produtos que ele encomendou com o que chegou.
4. O gerente clica para aceitar aprovar a injeção nas prateleiras.
5. O sistema cuida de avisar a parte de contagem do estoque sobre os números novos.

### Fluxos Alternativos / Exceções
- FA01 — Chegou produto de marca diferente e não existe na farmácia ainda. O sistema vai exigir que o gerente crie um novo cadastro.
- FA02 — A nota fiscal informada já havia sido lançada antes. O sistema mostra que é lançamento duplicado e tenta impedir.

### Relacionamentos
- **Include:** UC08 (Atualizar Estoque).  
- **Extend:** Nenhum.

---

## **UC08 — Atualizar Estoque**
**Ator(es):** Sistema  
**Descrição:** Atualização instantânea na contagem das caixas de remédios e perfumaria, que ajuda a saber quando acabou.  
**Pré-condições:** Terminar a entrada de uma nova nota aprovada, ou quando finaliza uma saída de clientes no caixa.  
**Pós-condições:** A quantidade visível pro saldo total foi atualizada pros caixas.  

### Fluxo Principal
1. O sistema repara que uma compra do gerente acabou de ocorrer.
2. Ele anota um histórico informando "Chegou entrega" naquele dia.
3. Aumenta a quantidade na visão global pro sistema deixar o cliente comprar na frente da loja.

### Fluxos Alternativos / Exceções
- FA01 — Fator zerado. O sistema avisa caso as caixinhas acabem antes da conta física devido a perdas.
- FA02 — Bateu no Estoque Mínimo. O computador manda uma lista amarela pro escritório comprar da distribuidora.

### Relacionamentos
- **Include:** UC08 - Atualizar Estoque (Sistema)
- **Extend:** Nenhum.

---

## **UC09 — Validar Receita**
**Ator(es):** Farmacêutico  
**Descrição:** Verificação técnica para avaliar se os carimbos ou exigências para vender antibióticos e controlados estão OK.  
**Pré-condições:** O sistema do caixa avistou um produto restrito.  
**Pós-condições:** A liberação oficial ocorreu e o cliente pode pagar a medicação.

### Fluxo Principal
1. O sistema trava os bip do Atendente e pede "Receituário Físico".
2. O farmacêutico que está na farmácia dá uma olhada na prescrição e no médico.
3. Ele escreve do seu próprio computador as credenciais e registro do profissional.
4. Pronto, as checagens atestam veracidade e fica retida pro governo a versão, destrancando o fluxo da venda.

### Fluxos Alternativos / Exceções
- FA01 — Papel amassado, médico não identificado ou receita de prazo vencido. O Farmacêutico vai em Invalidar a prescrição e o sistema solta e não inclui o remédio.
- FA02 — O cliente nem sequer foi a um posto de saúde e não tem receita. O Farmacêutico nega o processo de forma idêntica.

### Relacionamentos
- **Include:** UC09 - Validar Receita (Farmacêutico)
- **Extend:** UC01 Para remedios controlados.

---

## **UC10 — Cadastrar Produto**
**Ator(es):** Gerente  
**Descrição:** Formulário completo e fácil que indica ao computador da farmácia novos itens para seu controle central.  
**Pré-condições:** Ser um gerente tentando fazer o cadastro.  
**Pós-condições:** Nasce um novo produto etiquetável com dados de venda pra farmácia.

### Fluxo Principal
1. O gerente acessa no escritório a tela de criar mercadorias.
2. Preenche de qual laboratório vem, nome que vai ficar na nota, categorias gerais.
3. Mostra os fornecedores originais ou as origens dessa carga.
4. Por fim salva para começar a espalhar os produtos para todo terminal de balcão da farmácia que existir.

### Fluxos Alternativos / Exceções
- FA01 — O Gerente clica para salvar, sem dar um preço estipulado de venda. O sistema não o deixa terminar isso e grifa em vermelho onde precisa escrever.
- FA02 — O gerente erra e cadastra um remédio de fralda com o código de barra de pomada. O sistema dá um alerta forte falando que alguém já tem e ele tenta cancelar.

### Relacionamentos
- **Include:** UC10 - Cadastrar Produto (Gerente)

- **Extend:** Nenhum (só possui operações bases).
