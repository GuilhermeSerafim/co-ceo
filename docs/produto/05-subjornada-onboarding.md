# Subjornada de Onboarding do MVP Co-CEO

## Objetivo

Este documento detalha a subjornada de onboarding do MVP do Co-CEO.

O objetivo do onboarding nao e configurar a plataforma inteira. O objetivo e levar o empreendedor ate o primeiro valor percebido com o menor atrito possivel:

> conectar canais minimos, definir limites basicos, escolher o que nao sera supervisionado e receber o primeiro briefing util.

O onboarding deve ser progressivo. Ele coleta o essencial no inicio e deixa o Co-CEO aprender com validacoes, correcoes e memorias candidatas ao longo do uso.

## Posicao na Jornada Macro

Esta subjornada deriva da jornada macro descrita em `02-jornada-macro-mvp.md`.

Ela detalha o trecho:

- criar conta;
- onboarding inicial;
- conectar WhatsApp;
- conectar Agenda;
- definir horarios de briefing;
- definir regras, limites e assuntos sensiveis;
- fazer leitura inicial de contexto;
- gerar primeiro briefing;
- validar, corrigir ou ignorar;
- ativar rotina diaria.

## Taxonomia Usada

O onboarding e um workflow, nao um funcionario de IA.

Forma correta de abstrair:

- **Workflow**: Onboarding.
- **Agente condutor**: Agente de Onboarding.
- **Agentes auxiliares**: Agente de WhatsApp, Agente de Agenda, Agente de Memoria, Agente de Sintese e Agente de Aprovacao.
- **Funcionario de IA relacionado**: Secretaria ExecutivIA.
- **Interface de configuracao**: Painel web.
- **Interface de validacao e rotina**: WhatsApp.

O usuario nao precisa ver todos esses agentes. Para ele, a experiencia deve parecer simples:

> "Estou ativando meu Co-CEO e ensinando o que ele pode ou nao observar."

## Principio do Onboarding Progressivo

O onboarding deve seguir tres principios:

1. Coletar apenas o minimo necessario antes do primeiro valor.
2. Proteger privacidade antes de qualquer leitura por IA.
3. Transformar correcoes do usuario em aprendizado validavel.

Na pratica:

- perguntas fixas definem limites iniciais;
- perguntas geradas por IA calibram contexto real depois das conexoes;
- memorias importantes so viram regra apos validacao;
- acoes sensiveis nao sao executadas sem aprovacao humana.

## Fluxo Geral

```mermaid
flowchart TD
    A["Usuario cria conta"] --> B["Boas-vindas e explicacao de privacidade"]
    B --> C["Conectar WhatsApp"]
    C --> D{"WhatsApp conectado?"}

    D -->|Sim| E["Carregar conversas e contatos para selecao"]
    D -->|Nao| D1["Orientar reconexao ou fallback manual"]

    E --> F["Usuario escolhe contatos e grupos nao supervisionados"]
    F --> G["Usuario escolhe contatos e grupos prioritarios"]
    G --> H["Conectar Agenda"]

    H --> I{"Agenda conectada?"}
    I -->|Sim| J["Validar acesso a eventos"]
    I -->|Nao| I1["Seguir com WhatsApp apenas"]

    J --> K["Perguntas fixas de configuracao"]
    I1 --> K
    D1 --> K

    K --> L["Aplicar limites de escopo"]
    L --> M["Agente de Onboarding solicita leitura inicial permitida"]
    M --> N["Gerar ate 3 perguntas de calibracao por IA"]
    N --> O["Usuario responde ou pula perguntas"]
    O --> P["Gerar primeiro briefing"]
    P --> Q{"Usuario valida?"}

    Q -->|Aprova| R["Registrar preferencias confirmadas"]
    Q -->|Corrige| S["Criar memoria candidata ou ajuste de regra"]
    Q -->|Ignora| T["Ativar rotina basica sem assumir aprovacao"]

    R --> U["Onboarding concluido"]
    S --> U
    T --> U
```

## Etapas do Onboarding

### 1. Criacao de Conta

O usuario cria conta e entra no painel web.

Nesta etapa, o sistema deve explicar em linguagem simples:

- o que o Co-CEO vai observar;
- que o WhatsApp e o nucleo do MVP;
- que contatos/grupos podem ser excluidos da supervisao;
- que comunicacoes sensiveis exigem aprovacao;
- que o primeiro objetivo e gerar um briefing util.

### 2. Consentimento e Privacidade

Antes da conexao com WhatsApp, o usuario precisa entender que o Co-CEO podera acessar mensagens e metadados dentro do escopo permitido.

O texto deve deixar claro:

- o usuario pode excluir contatos e grupos da supervisao;
- o sistema nao deve processar conversas excluidas com IA;
- o usuario pode revisar limites depois;
- o Co-CEO nao envia comunicacoes sensiveis sem aprovacao no MVP.

### 3. Conexao do WhatsApp

O usuario conecta o WhatsApp.

Na arquitetura considerada, o Baileys e usado para leitura/espelhamento. O Baileys se conecta via WhatsApp Web e Linked Devices, nao via WhatsApp Business API oficial.

Depois da conexao, o sistema deve carregar dados suficientes para permitir selecao de escopo:

- conversas individuais;
- grupos;
- nomes conhecidos quando disponiveis;
- identificadores internos;
- recencia aproximada;
- volume aproximado.

O sistema deve evitar processamento por IA antes da escolha de escopo.

### 4. Selecao do Que Nao Sera Supervisionado

Esta e uma etapa central do onboarding.

O usuario deve escolher:

- contatos que o Co-CEO nao deve supervisionar;
- grupos que o Co-CEO nao deve supervisionar;
- conversas pessoais, familiares ou sensiveis;
- conversas que nao devem entrar em resumo, memoria, classificacao ou briefing.

Esses itens entram em uma denylist.

Regra de produto:

> Conversas excluidas nao devem ser enviadas para IA, nao devem gerar resumo, nao devem gerar memoria e nao devem aparecer em briefings.

### 5. Selecao de Contatos Prioritarios

Depois da denylist, o usuario escolhe contatos e grupos importantes.

Exemplos:

- socios;
- clientes principais;
- leads importantes;
- fornecedores criticos;
- equipe interna;
- contador;
- advogado;
- assistente humano.

Esses itens entram em uma lista de prioridade. A lista nao significa envio automatico nem acao autonoma. Ela apenas ajuda o Co-CEO a entender relevancia.

### 6. Conexao da Agenda

O usuario conecta Google Calendar ou outra agenda disponivel.

No MVP, a Agenda e apoio contextual. Ela serve para:

- identificar reunioes futuras;
- cruzar participantes com conversas permitidas do WhatsApp;
- preparar briefing pre-reuniao;
- sugerir pontos a lembrar.

Se a Agenda nao conectar, o onboarding pode continuar, mas o usuario deve saber que a preparacao de reuniao sera limitada.

### 7. Perguntas Fixas

O onboarding deve ter poucas perguntas fixas, agrupadas no painel.

Recomendacao para o MVP:

> 8 perguntas fixas no maximo.

Perguntas fixas recomendadas:

1. Quais conversas ou grupos o Co-CEO nao deve supervisionar?
2. Quais contatos ou grupos sao prioritarios?
3. Em quais horarios voce quer receber briefings?
4. Quais assuntos sempre exigem aprovacao humana?
5. Que tipo de resposta o Co-CEO pode sugerir, mas nao enviar sozinho?
6. Qual tom de comunicacao voce prefere?
7. Que tipo de reuniao merece preparacao automatica?
8. O que voce quer reduzir primeiro: ruido, esquecimento, follow-up, reunioes despreparadas ou respostas demoradas?

Essas perguntas criam a configuracao inicial.

### 8. Leitura Inicial Permitida

Depois das perguntas fixas e da selecao de escopo, o Agente de Onboarding pode solicitar uma leitura inicial permitida.

Essa leitura deve considerar apenas:

- conversas nao excluidas;
- contatos prioritarios;
- metadados permitidos;
- eventos de agenda permitidos;
- respostas fixas do usuario;
- politicas de aprovacao do MVP.

O objetivo nao e entender a vida inteira do empreendedor. O objetivo e gerar contexto suficiente para o primeiro briefing e para perguntas de calibracao.

### 9. Perguntas Geradas por IA

Depois da leitura inicial permitida, o Agente de Onboarding pode gerar perguntas de calibracao.

Recomendacao para o MVP:

> ate 3 perguntas geradas por IA no onboarding inicial.

Essas perguntas devem ser opcionais e altamente contextuais.

Exemplos:

- "Joao aparece com frequencia nas conversas permitidas. Ele e cliente, parceiro, fornecedor ou equipe?"
- "Esse grupo parece ter muito movimento. Quer que eu avise apenas quando houver mencao direta, decisao ou pendencia?"
- "Reunioes com clientes devem receber briefing 1 hora antes?"
- "Esse contato parece relacionado a proposta comercial. Ele deve entrar como prioridade?"
- "Quando alguem pedir status de entrega, voce prefere resposta objetiva ou mais consultiva?"

As perguntas geradas por IA nao devem ser ilimitadas. Se o sistema tiver muitas duvidas, deve priorizar as que mais impactam o primeiro briefing.

### 10. Primeiro Briefing

O primeiro briefing e o primeiro momento forte de valor.

Ele deve mostrar algo como:

- principais conversas relevantes;
- pendencias percebidas;
- reunioes proximas;
- pontos que talvez precisem de decisao;
- sugestoes de proximos passos;
- limites que ainda precisam de confirmacao.

O primeiro briefing nao deve ser longo. Ele precisa ser util, claro e corrigivel.

### 11. Validacao do Usuario

O usuario pode:

- aprovar;
- corrigir;
- ignorar;
- pedir para remover um contato;
- marcar algo como ruido;
- confirmar uma regra;
- rejeitar uma memoria candidata.

Essa validacao alimenta a memoria operacional.

## Perguntas Fixas vs Perguntas Geradas por IA

### Perguntas Fixas

Perguntas fixas servem para regras essenciais que nao dependem de analise de contexto.

Elas definem:

- permissao;
- escopo;
- horarios;
- assuntos sensiveis;
- tom;
- prioridade;
- objetivo inicial.

Elas devem ser previsiveis, auditaveis e iguais para todos os usuarios do MVP.

### Perguntas Geradas por IA

Perguntas geradas por IA servem para calibrar o Co-CEO com base no contexto real do usuario.

Elas devem surgir apenas depois de:

- WhatsApp conectado;
- contatos/grupos excluidos definidos;
- Agenda conectada ou explicitamente pulada;
- leitura inicial permitida concluida.

Elas devem ter limite e criterio.

No MVP:

- maximo de 3 perguntas no onboarding inicial;
- perguntas sempre opcionais;
- perguntas devem explicar por que estao sendo feitas;
- respostas podem virar memoria candidata, nunca regra sensivel automatica sem validacao.

## Papel do Agente de Onboarding

O Agente de Onboarding conduz o workflow de ativacao inicial.

Responsabilidades:

- guiar o usuario pelas etapas;
- chamar o Agente de WhatsApp para listar conversas e contatos;
- chamar o Agente de Agenda para validar eventos;
- aplicar regras de escopo antes de qualquer leitura por IA;
- chamar o Agente de Memoria para registrar configuracoes e memorias candidatas;
- chamar o Agente de Sintese para gerar o primeiro briefing;
- acionar a camada de Aprovacao quando houver regra sensivel.

O Agente de Onboarding nao e um funcionario de IA. Ele e um agente tecnico interno.

## Contexto Necessario Para o Agente

O Agente de Onboarding precisa de contexto, mas nao precisa de fine-tuning no MVP.

### Nao Precisa no MVP

- fine-tuning;
- treinamento proprio;
- RAG pesado de documentos;
- autonomia ampla.

### Precisa no MVP

- prompt de sistema bem definido;
- politica de produto do Co-CEO;
- regras de aprovacao humana;
- taxonomia de contatos, grupos e assuntos;
- respostas fixas do usuario;
- denylist e priority list;
- eventos de agenda permitidos;
- conversas permitidas;
- memorias confirmadas;
- memorias candidatas;
- schema de saida estruturada.

### RAG ou Recuperacao Contextual

No MVP, o mais correto e falar em recuperacao contextual operacional, nao em RAG pesado.

O sistema deve buscar contexto em bases internas:

- configuracoes do usuario;
- memorias confirmadas;
- conversas permitidas;
- agenda;
- decisoes anteriores;
- regras de aprovacao.

Essa recuperacao pode usar busca relacional, filtros por tempo, busca semantica ou combinacao das tres.

## Memoria no Onboarding

O onboarding cria tres tipos de informacao:

### Configuracao Confirmada

Informacoes explicitamente definidas pelo usuario.

Exemplos:

- horarios de briefing;
- contatos excluidos;
- contatos prioritarios;
- assuntos sensiveis;
- tom preferido.

### Memoria Candidata

Informacoes inferidas ou sugeridas pelo sistema, mas ainda nao confirmadas.

Exemplos:

- "Joao parece ser cliente importante";
- "Grupo X parece ter muito ruido";
- "Reunioes com cliente talvez precisem briefing 1 hora antes".

### Memoria Confirmada

Informacoes aceitas ou corrigidas pelo usuario.

Exemplos:

- "Joao e cliente estrategico";
- "Grupo X so deve gerar alerta quando houver mencao direta";
- "Reunioes comerciais recebem briefing 1 hora antes".

Regra:

> Memoria candidata nao deve ser usada como verdade operacional sensivel.

## Tratamento de Contatos e Grupos

Cada conversa pode ter um status operacional.

```txt
excluded      = nao supervisionar
priority      = supervisionar com alta relevancia
normal        = supervisionar normalmente
unknown       = aguardar mais contexto
needs_review  = pedir confirmacao ao usuario
```

O sistema deve permitir revisao posterior.

Exemplos:

- mover contato de normal para excluded;
- mover grupo de priority para normal;
- confirmar contato unknown como cliente;
- marcar grupo como ruido.

## Consideracoes Tecnicas Sobre Baileys

O Baileys permite receber eventos de mensagens, chats, contatos e grupos.

Pontos relevantes para o onboarding:

- o Baileys pode entregar historico inicial de chats, contatos e mensagens via `messaging-history.set`;
- eventos em tempo real chegam por `messages.upsert`;
- eventos de chat, contato e grupo ajudam a montar a lista inicial de supervisao;
- a configuracao `shouldIgnoreJid` permite ignorar um JID, fazendo com que eventos daquele JID nao sejam disparados e mensagens daquele JID nao sejam descriptografadas;
- `shouldSyncHistoryMessage` pode controlar processamento de historico;
- a aplicacao tambem deve manter sua propria denylist, pois a decisao de produto precisa existir acima da biblioteca.

Decisao recomendada para o MVP:

> O Co-CEO deve aplicar filtros de escopo antes de qualquer processamento por IA. Mesmo que mensagens ou metadados sejam recebidos tecnicamente, conversas excluidas nao devem ser resumidas, classificadas, vetorizadas ou memorizadas.

Referencias:

- [Baileys Introduction](https://baileys.wiki/docs/intro/)
- [Baileys SocketConfig](https://baileys.wiki/docs/api/type-aliases/SocketConfig/)
- [Baileys History Sync](https://baileys.wiki/docs/socket/history-sync/)
- [Baileys Receiving Updates](https://baileys.wiki/docs/socket/receiving-updates/)

## Falhas e Excecoes

### WhatsApp Nao Conecta

O sistema deve:

- orientar reconexao;
- permitir tentar novamente;
- explicar que sem WhatsApp o MVP perde o nucleo de valor;
- oferecer fallback manual apenas se fizer sentido para demonstracao.

### Lista de Contatos Incompleta

O sistema deve:

- mostrar o que conseguiu identificar;
- permitir busca manual;
- permitir adicionar exclusoes depois;
- marcar contatos desconhecidos como `unknown`.

### Usuario Nao Escolhe Excluidos

O sistema deve pedir confirmacao explicita:

> "Voce confirma que nao deseja excluir nenhuma conversa da supervisao?"

Sem essa confirmacao, a leitura inicial por IA nao deve avancar.

### Agenda Nao Conecta

O onboarding pode continuar.

O sistema deve deixar claro:

- briefings diarios continuam possiveis;
- preparacao de reuniao fica limitada;
- a Agenda pode ser conectada depois.

### Usuario Pula Perguntas de IA

O onboarding continua.

Perguntas puladas podem voltar como calibracao futura, se ainda forem relevantes.

### Primeiro Briefing Ruim

Se o primeiro briefing estiver ruim, o usuario deve conseguir corrigir rapidamente:

- "isso e ruido";
- "esse contato nao deve ser supervisionado";
- "isso e importante";
- "esse tom esta errado";
- "nao use essa memoria".

## Criterio de Onboarding Concluido

O onboarding e considerado concluido quando:

- conta criada;
- WhatsApp conectado ou fallback explicitamente aceito;
- contatos/grupos excluidos revisados ou confirmados como vazios;
- contatos/grupos prioritarios definidos ou pulados;
- horarios de briefing definidos;
- regras basicas de aprovacao definidas;
- Agenda conectada ou pulada;
- primeiro briefing gerado;
- usuario aprovou, corrigiu ou ignorou conscientemente o primeiro briefing;
- rotina diaria ativada.

## O Que Nao Entra no Onboarding do MVP

Nao entra no onboarding inicial:

- configuracao profunda de CRM;
- financeiro;
- juridico;
- RH;
- marketing;
- automacoes autonomas;
- permissao ampla para envio sem aprovacao;
- mapeamento completo de todos os clientes;
- coleta extensa de dados da empresa;
- fine-tuning;
- treinamento personalizado de modelo.

Esses pontos podem aparecer depois como expansao, configuracao avancada ou proxima versao.

## Decisoes de Produto

- O onboarding deve ser progressivo.
- A selecao de contatos/grupos nao supervisionados vem antes da primeira leitura por IA.
- O usuario deve poder excluir conversas pessoais, familiares ou sensiveis.
- Perguntas fixas devem ser limitadas a 8 no MVP.
- Perguntas geradas por IA devem ser limitadas a 3 no onboarding inicial.
- Perguntas geradas por IA dependem de contexto permitido, nao de acesso irrestrito.
- O Agente de Onboarding conduz o workflow, mas nao e um funcionario de IA.
- O primeiro valor do onboarding e o primeiro briefing util.
- Memorias inferidas durante onboarding entram como candidatas ate validacao.
- Comunicacoes sensiveis continuam exigindo aprovacao humana.

## Proximos Artefatos Relacionados

Depois desta subjornada, as proximas etapas devem detalhar:

- subjornada do WhatsApp;
- subjornada de briefings;
- subjornada de preparacao de reuniao;
- subjornada de sugestao e aprovacao de resposta;
- subjornada de memoria operacional.

