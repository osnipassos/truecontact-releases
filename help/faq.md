# TrueContact — Manual do Usuário

> **Versão do documento:** Outubro 2026 (1.0.259)  
> Encontrou um erro ou tem uma pergunta não respondida? [Abra uma issue](https://github.com/osnipassos/truecontact-releases/issues).

---

## Índice

1. [Primeiros Passos](#1-primeiros-passos)
2. [Segurança e Privacidade](#2-segurança-e-privacidade)
3. [Sincronização de Contatos](#3-sincronização-de-contatos)
4. [Conectar o Google Contacts](#4-conectar-o-google-contacts)
5. [Conectar as fontes sociais (LinkedIn, Facebook, Instagram, X, Goodreads, TikTok, Duolingo e PDL)](#5-conectar-as-fontes-sociais-linkedin-facebook-instagram-x-goodreads-tiktok-duolingo-e-pdl)
6. [Conectar o WhatsApp e o Telegram](#6-conectar-o-whatsapp-e-o-telegram)
7. [Templates e Automações](#7-templates-e-automações)
8. [Operações em Lote e Indicadores](#8-operações-em-lote-e-indicadores)
9. [Histórico e Reversão](#9-histórico-e-reversão)
10. [Atualizações](#10-atualizações)

---

## 1. Primeiros Passos

### O que é o TrueContact?

O **TrueContact** é um CRM pessoal automático para Mac e Windows. Liga-se ao iCloud, ao Google Contacts, ao LinkedIn, ao Facebook e ao WhatsApp para **sincronizar, enriquecer e organizar** os seus contatos — e envia mensagens de aniversário e de acompanhamento automaticamente, em segundo plano.

Ao contrário das soluções cloud (HubSpot, Salesforce, etc.), o TrueContact roda **100% no seu computador**. Não há subscrição, não há conta, não há servidor para salvar os seus dados.

### Para quem é?

- Profissionais de networking que querem manter contatos sempre atualizados
- Quem usa o iPhone/Mac e quer aproveitar ao máximo o iCloud Contacts
- Quem usa o Gmail e precisa manter o Google Contacts em sincronia com o iCloud
- Quem quer enviar parabéns automáticos sem parecer um bot
- Quem valoriza a **privacidade total** dos seus dados de contato

### Requisitos do sistema

| Plataforma | Versão mínima |
|---|---|
| macOS | 13 Ventura ou superior |
| Windows | 10 (64-bit) ou superior |

### Como instalar

1. Acesse a [página de Releases](https://github.com/osnipassos/truecontact-releases/releases/latest)
2. Baixe o arquivo para o seu sistema operacional:
   - **macOS:** arquivo `.dmg`
   - **Windows:** arquivo `.exe` (instalador)
3. **macOS:** Abra o `.dmg`, arraste o TrueContact para a pasta Aplicações
4. **Windows:** Execute o instalador e siga os passos
5. Na primeira abertura, o **Assistente de Configuração** guia você por cada etapa

> **Importante (macOS):** Se o sistema mostrar o aviso "app de desenvolvedor desconhecido", vá a **Configurações do Sistema → Privacidade e Segurança** e clique em "Abrir na mesma". O TrueContact não está na App Store por opção — isso é intencional para manter o app gratuito.

### Assistente de Configuração (Onboarding Wizard)

Na primeira abertura, o TrueContact exibe um **assistente de configuração passo a passo** que guia você por todas as integrações:

1. **Boas-vindas** — visão geral do hub-and-spoke, idioma e fuso horário
2. **Apple iCloud** — inserção do Apple ID e App-Specific Password
3. **Google Contacts** — autenticação OAuth com a sua conta Google
4. **LinkedIn** — autenticação e configuração dos radares automáticos
5. **Facebook** — autenticação e varredura da lista de amigos
6. **WhatsApp** — leitura do QR Code
7. **Agendamento** — frequência e janela horária das varreduras automáticas
8. **Normalização** — prefixos, sufixos e formatos de nome
9. **Templates** — mensagens de aniversário personalizadas
10. **Alertas e Merge** — prévia do sistema de detecção de duplicados, com o auto-merge de alta fidelidade
11. **Tudo pronto!** — links de ajuda e feedback

Você pode rever o assistente a qualquer momento em **Configurações → Refazer Setup Inicial**.

### Primeira configuração manual (alternativa ao assistente)

Se preferir configurar manualmente:

1. **Configurar o iCloud** — insira o Apple ID e a App-Specific Password para importar os seus contatos
2. **Conectar o Google Contacts** — autorize via OAuth nas Configurações
3. **Conectar o LinkedIn e o Facebook** — faça login nas Configurações para ligar as fontes de enriquecimento
4. **Conectar o WhatsApp** — leia o QR Code nas Configurações para ativar o envio de mensagens
5. **Criar templates de aniversário** — defina as mensagens automáticas que o sistema vai enviar
6. **Deixar rodar** — o TrueContact faz tudo o resto em segundo plano

---

## 2. Segurança e Privacidade

### Como apagar todos os dados e começar do zero?

Em **Configurações → Configurações Gerais → Resetar banco de dados**. O TrueContact volta ao estado de recém-instalado e o assistente de configuração reaparece:

- **É apagado:** todos os contatos, grupos, filas, histórico de alterações, histórico de mensagens e mensagens agendadas.
- **É desconectado:** iCloud, Google, WhatsApp, LinkedIn, Facebook e a chave do PeopleDataLabs.
- **Continua como está:** suas preferências (limites, listas de normalização, agenda, idioma) e os modelos de mensagem.

Para evitar um clique acidental, é preciso digitar **RESETAR** para confirmar.

**Nada é apagado no iCloud nem no Google** — só o banco local do TrueContact. Quando você reconectar as contas, os contatos voltam a ser importados de lá.

Antes de apagar, o TrueContact salva uma cópia completa do banco atual na mesma pasta, com o nome `truecontact.db.backup-antes-do-reset-<data>` — só a mais recente é mantida. Para voltar atrás: com o TrueContact fechado, apague os arquivos `truecontact.db-wal` e `truecontact.db-shm` (se existirem) e renomeie a cópia para `truecontact.db`. No servidor Linux, o banco fica em `/var/lib/truecontact`.

### Os seus dados nunca saem do seu computador

Esta é a promessa central do TrueContact: **os seus dados são seus e ficam no seu computador**.

Toda a informação dos seus contatos — nomes, telefones, emails, notas, histórico de mensagens, fotos de perfil — é armazenada num banco de dados **SQLite local**, numa pasta de dados do aplicativo no seu disco rígido. Não existe nenhum servidor TrueContact que receba, processe ou armazene esses dados.

O banco de dados encontra-se em:

- **macOS:** `~/Library/Application Support/truecontact/database.sqlite`
- **Windows:** `%APPDATA%\truecontact\database.sqlite`

Você pode abrir, copiar ou fazer backup deste arquivo a qualquer momento com ferramentas como o [DB Browser for SQLite](https://sqlitebrowser.org/).

### O que é enviado para a internet?

O TrueContact apenas faz conexões com a internet para:

| Conexão | Finalidade | Os seus dados passam pelos servidores TrueContact? |
|---|---|---|
| iCloud CardDAV | Sincronizar contatos com o iCloud | **Não** — conexão direta Apple |
| Google People API | Sincronizar contatos com o Google Contacts | **Não** — conexão direta Google |
| LinkedIn | Ler perfis públicos dos seus contatos | **Não** — só leitura, sem envio |
| Facebook | Ler perfis e a sua lista de amigos | **Não** — só leitura, sem envio |
| WhatsApp Web | Enviar mensagens e ler fotos de perfil | **Não** — conexão direta WhatsApp |
| GitHub Releases | Verificar se há atualizações | **Não** — só verifica um número de versão |

**Nenhuma dessas conexões passa pelos servidores TrueContact** — porque esses servidores simplesmente não existem.

### Quanto espaço o TrueContact ocupa no disco?

Depende do número de contatos e, sobretudo, das fotos de perfil. Para referência, uma base com **8.500 contatos e 8.000 fotos ocupa cerca de 1 GB**.

O maior consumidor é o **histórico de alterações** — a cada mudança num contato, o TrueContact guarda uma cópia completa do estado anterior, para que você possa desfazer. Esses registros incluem a foto, e por isso crescem depressa: cerca de **30 MB por dia** numa base ativa.

Para evitar que o arquivo cresça sem limite, o TrueContact faz uma **limpeza automática todas as madrugadas, às 03:30**:

- snapshots com mais de **30 dias** são apagados;
- confirmações de envio (*"Replicado com sucesso"*) são apagadas após **2 dias**, porque não servem para desfazer nada.

O espaço é devolvido ao sistema imediatamente — o arquivo encolhe sozinho, sem qualquer ação da sua parte. Se o computador estiver suspenso às 03:30, a limpeza corre no arranque seguinte.

A interface mostra sempre os **últimos 30 snapshots** de cada contato, portanto a limpeza não afeta o que você vê no dia a dia.

Há ainda um **cache de miniaturas de fotos** (`media_cache/thumbs/`), criado para a lista de contatos abrir rápido: cerca de 3 KB por contato com foto (~25 MB numa base de 8.000 fotos). Ele se mantém sozinho — miniaturas de contatos excluídos são removidas diariamente, e o cache inteiro é regenerável: pode ser apagado a qualquer momento sem perda alguma.

> **Ajustar ou desligar:** as chaves `retencao_historico_dias` e `retencao_historico_ruido_dias` controlam os dois prazos. O valor `0` desliga a regra correspondente — o histórico passa a ser salvo indefinidamente e o arquivo cresce sem limite.

### Sessão do WhatsApp

Quando você liga o WhatsApp ao TrueContact através do QR Code, é gerado um **arquivo de sessão local** que mantém a sua autenticação. Este arquivo fica em:

- **macOS:** `~/Library/Application Support/truecontact/whatsapp-session/`
- **Windows:** `%APPDATA%\truecontact\whatsapp-session\`

> **Aviso:** Nunca compartilhe esta pasta com ninguém. Quem tiver acesso a estes arquivos pode enviar mensagens em seu nome. Se suspeitar de comprometimento, vá a **WhatsApp → Configurações → Dispositivos conectados** e remova a sessão TrueContact.

### App-Specific Password do iCloud

O TrueContact usa uma **App-Specific Password** para acessar o iCloud Contacts — nunca a sua senha principal do Apple ID. Se a senha for comprometida, você pode revogá-la sem alterar o seu Apple ID ou afetar o restante da conta.

Para gerar uma, vá a [appleid.apple.com](https://appleid.apple.com) → **Iniciar sessão e segurança → Senhas específicas de app**.

### Token OAuth do Google

O TrueContact usa **OAuth 2.0** para acessar o Google Contacts — você autoriza o acesso sem nunca inserir sua senha do Google. O token de acesso é armazenado localmente e pode ser revogado a qualquer momento em [myaccount.google.com/permissions](https://myaccount.google.com/permissions) → TrueContact.

---

## 3. Sincronização de Contatos

### Quanto tempo uma alteração leva para chegar ao iCloud e ao Google?

Segundos. Desde a versão 1.0.256, **toda alteração sai para os provedores assim que entra no TrueContact**: uma edição no painel, uma leitura do LinkedIn, um dado trazido pelo WhatsApp, um merge, uma reversão. O app junta o que mudou em 1,5 segundo e envia um contato por vez, para cada provedor em que ele está. Medido na prática: uma URL adicionada chegou ao iCloud e ao Google em 4 segundos.

Antes, a alteração esperava o radar de 5 minutos ou o fim do ciclo de leitura das redes, que pode levar 25 minutos.

Duas garantias:

- **Nada volta para a origem.** Uma alteração lida do Google não é reenviada ao Google por esse caminho; só vai para o iCloud, e vice-versa.
- **Se falhar, fica na fila.** O envio imediato é a primeira tentativa. O que não puder sair na hora (provedor fora, conflito de versão) continua na fila e é retentado pelo radar, como sempre.

A opção fica em **Configurações → Agendamento → Enviar alterações em seguida**, ligada por padrão. Desligada, tudo volta a esperar o radar.

### O TrueContact confere se o iCloud e o Google aceitaram o que foi enviado?

Sim, desde a 1.0.255. Logo depois de cada envio, o TrueContact **lê o contato de volta** do provedor (no iCloud, baixa o cartão; no Google, usa a resposta da própria gravação) e compara com o que mandou.

O que o provedor devolveu sem é tratado como **recusa do provedor**, não como exclusão sua. Esse item fica marcado como "teimoso" para aquele provedor: continua no TrueContact, continua indo para os outros provedores, e nenhuma leitura futura daquele provedor o apaga. Exemplo real: um endereço com a cidade grafada "maceioal" foi recusado pelo Google e permaneceu no TrueContact e no iCloud.

O retrato que o TrueContact guarda de cada contato em cada provedor passou a ser sempre o **real**, lido do provedor, e não mais o que foi enviado. É esse retrato que decide, nas leituras seguintes, o que foi uma exclusão feita por você.

### Uma fonte pode apagar um dado meu só porque não o trouxe?

Não. Depois de uma auditoria completa do histórico em outubro de 2026, as regras de remoção ficaram assim:

- **Só uma leitura completa do próprio provedor remove algo**, e só o que aquele provedor tinha mostrado numa leitura real anterior. O retrato guardado por um envio nosso não conta. Se o Google nunca mostrou um telefone, a ausência dele numa leitura do Google não apaga nada.
- **Leitura de rede social nunca esvazia campo.** LinkedIn, Facebook, Instagram e as demais só acrescentam. Uma leitura interrompida por lentidão fica fora do pacote em vez de entrar como lista vazia.
- **Empresa, cargo, aniversário, notas, apelido e foto** só são esvaziados por um provedor que já os tinha mostrado antes. A primeira leitura de um provedor recém-conectado não apaga nada.
- **Grupos seguem a mesma regra**, no Google e no iCloud: só sai do grupo quem o provedor já tinha listado numa leitura anterior. Se o seu iPhone regravar um grupo com menos membros do que o TrueContact enviou, os membros que o telefone não devolveu ficam no TrueContact e o grupo é reenviado.
- **Conflito de versão no iCloud** (o cartão mudou no aparelho depois da última leitura) adia o envio e lê o aparelho primeiro, em vez de sobrescrever a sua edição.

Tudo o que uma leitura remove continua aparecendo no histórico do contato, em vermelho, com a origem. Uma auditoria semanal confere se algo removido por iCloud ou Google ainda falta e se o outro provedor ainda o tem (veja a seção 9).

### Meus endereços foram corrigidos sozinhos. O que aconteceu?

Na 1.0.258 o TrueContact ganhou um conjunto de regras novas de normalização de endereços, resultado da análise dos 8 mil endereços de uma base real, e aplicou essas regras uma vez em toda a base. Cada contato alterado recebeu no histórico uma entrada **Sanitização → Normalização automática** com o antes e o depois, campo a campo.

O que as regras corrigem:

- **País no lugar da cidade** ("Brasil" no campo cidade) vai para o campo país. Com países diferentes nos dois campos ("Itália" na cidade e "Brasil" no país), nada é tocado: é contradição, não erro de campo.
- **Nome de estado no lugar da cidade** ("Paraná", "Santa Catarina", "Distrito Federal") vira a sigla no campo estado. São Paulo e Rio de Janeiro ficam, porque também são cidades.
- **Capital com UF errada** ("Curitiba, SP", "Porto Alegre, PR") recebe a UF correta da capital.
- **Estado com sobras** ("Sp | Brazil", "Sp.", "Capital", "Curitiba e Região", um site) é limpo. "Capital" com estado SP vira São Paulo.
- **Cidade com UF colada** ("Alphaville-sp", "Curitiba/pr") é separada em cidade e estado.
- **Localidade no campo de rua** com o estado no campo cidade ("Jundiaí | São Paulo") vira cidade Jundiaí, estado SP.
- **Rua que repete a cidade** ("São Luís e Região" numa linha cuja cidade já é São Luís) é esvaziada.
- **CEP de 7 dígitos em São Paulo** recebe o zero à esquerda que perdeu. "Complemento: Apartamento 71" dentro da rua vai para o campo complemento. Sites e e-mails dentro de campos de endereço saem.
- **Linhas vazias** somem, e um endereço cujos campos preenchidos são todos iguais aos de outro ("SP, Brasil" ao lado de "Osasco, SP, Brasil") é absorvido pelo mais completo, que herda o que só o descartado tinha.

O que as regras **não** fazem, de propósito: juntar duas ruas diferentes na mesma cidade (casa e trabalho), juntar duas cidades diferentes, mexer em estados estrangeiros ou decidir contradições reais, como "Florianópolis" na rua com "Curitiba" na cidade. Nesses casos a decisão é sua.

As mesmas regras valem para todo endereço que entra daqui em diante, de qualquer fonte.

### Como os grupos ficam iguais no iPhone, no Google e no TrueContact?

Um grupo é um só, com uma etiqueta correspondente no Google e um grupo no iCloud. Adicionar ou tirar um contato no TrueContact atualiza os dois provedores na hora. O que mudou em outubro de 2026:

- **Grupo novo no iPhone vira etiqueta nova no Google.** Até a 1.0.256, o TrueContact tentava adivinhar se o grupo novo era um grupo antigo renomeado e podia renomear a etiqueta errada no Google. Essa adivinhação foi removida. Renomear um grupo no iPhone ou no Google continua sendo reconhecido como renomeação.
- **O TrueContact só tira alguém de um grupo se o provedor já tinha listado essa pessoa** numa leitura anterior. Membros que você acabou de adicionar e o iPhone ainda não devolveu ficam, e o grupo é reenviado. Consequência: logo após instalar a 1.0.257, a primeira remoção feita no iPhone em cada grupo é desfeita uma vez; a partir da segunda leitura, vale.
- **Um grupo do iCloud que o TrueContact não conhece** (por exemplo, uma cópia que sobrou de grupos duplicados) é importado com os membros que estão no aparelho, em vez de ser ignorado para sempre.
- Se o Google recusar adicionar alguém a uma etiqueta, o motivo vai para o log do painel.

### Posso criar um grupo novo direto na ficha do contato?

Sim, desde a 1.0.257. No botão **+ Grupo** da ficha, digite o nome. Se não existir grupo com esse nome, a primeira linha da lista oferece **Criar grupo "Nome" e adicionar**. Enter também cria quando a busca não tem resultados. O grupo nasce no TrueContact, ganha o cartão no iCloud e a etiqueta no Google, e o contato já entra nele. Maiúsculas e espaços duplicados são ignorados na comparação, então "clientes vip" reaproveita um "Clientes VIP" existente.

### Dá para buscar um contato pelo @ da rede social?

Sim. A busca do topo encontra contatos pelo nome de usuário de qualquer rede, com ou sem o @. Também aceita nome do meio, palavras em qualquer ordem e sem acento.

### O nome de um contato pode ser trocado por uma rede social?

Não, com uma exceção. A regra vigente:

- **Trocam o nome:** LinkedIn (fonte oficial do nome profissional), iCloud e Google (as suas agendas). O LinkedIn junta o nome atual com o dele e, quando o nome do LinkedIn já contém todas as palavras do atual, vale o do LinkedIn inteiro, na ordem dele.
- **Facebook** troca o nome só quando o contato não tem LinkedIn.
- **Todo o resto só dá nome ao contato que cria:** X, Instagram, TikTok, Goodreads, Duolingo, Telegram e WhatsApp. O nome de exibição dessas redes costuma ser apelido ou marca ("Eltonminetto.dev", "Heitor Kuser Mercado Imobiliário Global").
- **O merge nunca mistura nomes.** O nome do contato que vence o merge é mantido inteiro: primeiro nome, nome do meio e sobrenome vêm do mesmo contato. Até a 1.0.258 o merge automático pegava campo a campo, e um nome do meio vazio podia receber o do outro contato.
- Redes sociais também **não marcam nem desmarcam um contato existente como empresa**; só o contato que elas mesmas criam. Uma conta de empresa no X ou uma página comercial no Facebook não transformam a sua agenda.

### Por que um site aparece riscado com ⚠️ no contato?

O TrueContact testa os sites dos contatos e risca os que **comprovadamente não existem**: domínio que não existe mais ou página que responde "não encontrada" (404). Sites que só bloqueiam acesso automático (proteção anti-robô como a do Cloudflare), que estão fora do ar momentaneamente ou com certificado vencido **não** são riscados — o site existe, só não deixou o TrueContact ver. Sites riscados são testados de novo toda madrugada e voltam ao normal sozinhos se responderem. Nada é apagado.

### Qual foto o TrueContact usa quando várias redes têm foto?

A do **LinkedIn** é a preferencial. Se o contato tem perfil no LinkedIn e já tem foto, nenhuma outra fonte (Goodreads, Telegram, Duolingo, TikTok, X, WhatsApp…) troca essa foto — elas só preenchem quando o contato está sem foto. Uma foto escolhida por você (no iPhone, no Google, no painel ou no merge) continua sendo respeitada, e o botão de enriquecimento manual pode trocar a foto quando você pedir.

### Como filtrar os contatos por fonte (Instagram, Duolingo, WhatsApp…)?

Abra **Filtros** na lista de contatos. No bloco **Fontes** há, para cada fonte, um par **Com** e **Sem**: LinkedIn, Facebook, Instagram, X (Twitter), Goodreads, TikTok, Duolingo, WhatsApp, Telegram e PDL. Para as redes sociais vale ter o perfil daquela rede no contato; para o WhatsApp, ter um telefone confirmado no WhatsApp; para o PDL, o contato já ter sido consultado. Os filtros se combinam — por exemplo, **Com Duolingo** + **Sem LinkedIn** lista quem veio só do Duolingo.

### O que dá para ajustar na aba Normalização?

A aba **Configurações → Normalização** reúne tudo o que o TrueContact limpa e valida automaticamente:

- **Nomes** — prefixos de tratamento, sufixos acadêmicos e familiares, e **palavras-fantasma**: termos que o cache do iCloud insiste em devolver grudados aos nomes e que você quer remover sempre.
- **Deduplicação** — liga/desliga o merge automático de duplicados óbvios.
- **Validação de dados** — liga/desliga a verificação em segundo plano de domínios de e-mail (MX) e sites (HTTP), e a lista de domínios considerados "pessoais" (gmail, uol…) na classificação casa × trabalho.
- **Histórico e retenção** — o horário em que a manutenção diária roda (03:30 por padrão), por quantos dias os snapshots e as confirmações de envio ficam no histórico (0 desliga a limpeza) e quanto um e-mail ou site marcado espera antes de ser re-testado.
- **Revalidação automática** — na manutenção das 03:30, o TrueContact re-testa os e-mails e sites que estão marcados como "não responde" e **remove a marcação** dos que voltaram a funcionar. Nada é apagado: um e-mail com domínio fora do ar continua no contato, apenas tachado e com um aviso — apagar é sempre decisão sua, no painel. Perfis sociais que a rede responde como inexistentes (404) também são só marcados, nunca removidos. A única remoção da seção é a opção (desligada por padrão) de mover contatos completamente vazios para a lixeira, que é reversível.


### Excluí, fundi ou restaurei um contato — isso fica registrado em algum lugar?

Sim. A partir da versão seguinte à 1.0.129, o painel de **Histórico** de cada contato registra também os eventos de ciclo de vida, com ícone e origem próprios:

- **Enviado para a lixeira** — seja pela exclusão no painel, por um merge (o contato duplicado que foi absorvido ganha o registro "Fundido em…") ou pelos radares, quando o contato é apagado diretamente no iCloud ou no Google Contacts.
- **Restaurado da lixeira** — tanto pela restauração manual quanto ao desfazer um merge.

Outras melhorias no mesmo pacote:

- **Fundir contatos não exige mais o iCloud.** Antes, o contato vencedor precisava ter mapeamento Apple; agora o merge funciona com contatos que existem só no Google ou só no TrueContact.
- **Restaurar e reverter atualizam todos os serviços.** Qualquer recuperação (restauração da lixeira, reversão de histórico, desfazer merge) reenvia o contato para **todos** os provedores conectados — iCloud e Google — e não apenas para o iCloud.
- **Reverter é fiel.** O registro de uma reversão agora retrata exatamente o estado em que o contato ficou, incluindo o que foi removido — reversões futuras partem do retrato certo.

### Apaguei um telefone/e-mail no iPhone ou no Google — ele some de todos os lugares?

Sim, automaticamente. Quando você apaga um dado em um provedor conectado, o TrueContact
detecta a exclusão na próxima leitura e a propaga para o Hub e para os demais provedores —
a exclusão "cola", sem o dado teimar em voltar. A remoção fica registrada no histórico do
contato, de onde pode ser revertida dentro do período de retenção.

Há uma proteção embutida: quando um provedor **descarta repetidamente** um dado que o
TrueContact devolve (o iCloud faz isso com certos endereços e mensageiros antigos), o
sistema reconhece o padrão e **não** trata como exclusão sua — o dado fica preservado no
Hub, apenas marcado. Nenhuma falha de leitura apaga nada: a detecção só acontece em
leituras completas do provedor.

### Alterei um contato — por que todas as fontes dele foram atualizadas?

Quando o TrueContact detecta uma **alteração real** em um contato — uma edição feita no iPhone/iCloud, no Google Contacts, no próprio painel do TrueContact, ou um dado novo trazido por uma das redes (LinkedIn, Facebook, Instagram, X ou WhatsApp) — ele aproveita o momento e agenda uma atualização de **todas as outras fontes vinculadas** àquele contato: os perfis sociais entram na fila de enriquecimento e os telefones voltam para verificação no WhatsApp.

Isso mantém o contato inteiro em dia de uma vez só, com três proteções:

- **Só alteração de verdade conta.** O eco da própria sincronização (por exemplo, o iCloud devolvendo um dado que o TrueContact acabou de enviar) é reconhecido e **não** dispara nada — o mesmo filtro que o painel de Histórico usa para não poluir a linha do tempo.
- **No máximo uma vez por dia.** Uma fonte que já foi verificada hoje não volta para a fila, não importa quantas alterações aconteçam — sem laços infinitos entre as redes.
- **Prioridade baixa.** Essas atualizações entram no fim da fila e respeitam os limites por ciclo de cada rede; um pedido seu feito diretamente no painel sempre passa na frente.

No Histórico do contato, essas atualizações aparecem com a origem de quem as disparou (ex.: `cascata_apple` quando o gatilho foi uma edição no iCloud).

### Arquitetura Hub-and-Spoke

O TrueContact funciona como um **Hub central** (base de dados SQLite local), com dois tipos de conectores:

**Provedores bidirecionais** (leem e escrevem contatos):
- **Apple iCloud** — via CardDAV
- **Google Contacts** — via Google People API

**Fontes de enriquecimento** (apenas leitura, adicionam dados):
- **LinkedIn** — cargo, empresa, foto de perfil, redes sociais, data de conexão
- **Facebook** — foto de perfil, cidade, sites, telefone, e-mail, relacionamentos e data de amizade
- **WhatsApp** — foto de perfil, nome de exibição e, nas contas comerciais, e-mail, endereço, site e perfis de Facebook e Instagram

O processo de sincronização funciona assim:

1. **Pull do iCloud** — Lê todos os contatos e grupos via CardDAV, preservando ETags para detectar alterações
2. **Pull do Google** — Lê alterações desde o último sync via SyncToken
3. **Enriquecimento LinkedIn** — Para contatos com perfil LinkedIn, importa cargo, empresa, foto e redes sociais
4. **Enriquecimento Facebook** — Para contatos com perfil do Facebook, importa foto, cidade, sites e o que estiver público no "Sobre"
5. **Enriquecimento WhatsApp** — Para contatos com número de telefone, importa a foto de perfil em alta resolução e, quando o número pertence a uma **conta comercial**, também o e-mail, o endereço, o site e os perfis de Facebook e Instagram do negócio. Conversas com números que ainda não estavam na sua agenda viram contatos novos, já com o nome do perfil
6. **Push para iCloud e Google** — Escreve as alterações de volta em ambos os provedores

> **Regra fundamental:** O TrueContact **nunca apaga dados manuais**. Se adicionar uma nota ou um email a um contato no iPhone, essa informação é preservada mesmo que o LinkedIn devolva um campo vazio.

### De onde veio cada dado?

Com tantas fontes escrevendo no mesmo contato, saber a procedência de cada campo deixa de ser detalhe. Por isso **cada campo exibe um pequeno ícone de origem** — no nome, na foto, no cargo, na empresa, nos telefones, e-mails, endereços, datas, notas, grupos e relacionamentos:

| Ícone | Significa |
|---|---|
| Apple | Veio do iCloud Contacts |
| Google | Veio do Google Contacts |
| LinkedIn | Importado do perfil do LinkedIn |
| Facebook | Importado do perfil do Facebook |
| WhatsApp | Veio do WhatsApp (foto, nome ou perfil Business) |
| Lápis | Editado manualmente por você |
| Setas convergindo | Resultado de uma fusão de contatos |

Passe o mouse sobre o ícone para ver o nome da fonte. É esse mesmo rastro que permite ao sistema decidir quem pode sobrescrever o quê — e permite a você identificar rapidamente um dado que chegou errado de uma rede social.

### Limpeza automática dos dados

Contatos acumulados ao longo de anos trazem sujeira: o mesmo telefone gravado duas vezes em formatos diferentes, e-mails com espaços e caracteres inválidos, datas sem ano duplicando datas completas, endereços que contêm apenas o nome do país.

O TrueContact corrige isso sozinho, tanto na entrada quanto no que já está gravado:

- **Telefones** — prefixo internacional antigo, código de operadora e dois números colados num só campo são desfeitos; duplicados que só diferem no nono dígito são unificados
- **E-mails** — validação real do endereço e rótulo (casa/trabalho) inferido pelo domínio
- **Datas** — uma data sem ano é descartada quando a mesma data com ano já existe com o mesmo rótulo
- **Endereços** — um endereço que só declara o país é descartado quando outro já declara o mesmo país
- **Redes sociais** — URLs equivalentes são deduplicadas, e slugs que deixaram de existir (404) são marcados

Cada uma dessas correções fica registrada no histórico do contato, com o ícone de limpeza automática — nada acontece em silêncio.

### Grupos sincronizados entre iCloud e Google

Os grupos de contatos são sincronizados entre os dois provedores:

- Um grupo criado no iCloud aparece automaticamente no Google Contacts
- Membros adicionados/removidos de um grupo propagam para ambos os lados
- Renomear um grupo num provedor atualiza automaticamente o outro

### Redes Sociais suportadas

O TrueContact normaliza e armazena perfis de:

| Rede | Formato armazenado |
|---|---|
| LinkedIn | `linkedin.com/in/<slug>` |
| Instagram | `instagram.com/<handle>` |
| **Threads** | `threads.net/@<handle>` |
| Twitter/X | `twitter.com/<handle>` |
| GitHub | `github.com/<handle>` |
| TikTok | `tiktok.com/@<handle>` |
| Facebook | `facebook.com/<slug>` |
| YouTube | `youtube.com/@<handle>` |
| Pinterest | `pinterest.com/<handle>` |
| Gravatar | `gravatar.com/<handle>` |
| Goodreads | `goodreads.com/<vanity>` ou `goodreads.com/user/show/<id>-<nome>` |
| Duolingo | `duolingo.com/profile/<usuario>` |
| Telegram | `t.me/<usuario>` ou, sem @usuário, `t.me/+<número>` |

### Normalização de números de telefone

Para unir corretamente um contato do iCloud com a sua conta WhatsApp, o sistema precisa comparar números de telefone. O mesmo número pode estar salvo de formas muito diferentes:

| Formato no iCloud | Formato no WhatsApp |
|---|---|
| `(11) 98765-4321` | `5511987654321` |
| `+55 11 9 8765-4321` | `5511987654321` |
| `11 8765-4321` (sem 9º dígito) | `5511987654321` |

O TrueContact normaliza automaticamente todos estes formatos, incluindo a adição do **9º dígito** para números brasileiros mais antigos.

### Por que não vejo a foto de alguns contatos do WhatsApp?

**O WhatsApp respeita as configurações de privacidade de cada usuário.** Se um contato configurou a sua foto de perfil para ser visível apenas para os seus próprios contatos (ou para ninguém), o WhatsApp não disponibiliza essa foto a nenhum aplicativo. O TrueContact mostra um **ícone de privacidade** nesse caso — isso é comportamento correto, não um bug.

> **Dica:** Se quiser ver a foto real de um contato específico, peça-lhe que abra as configurações de privacidade do WhatsApp → Foto de perfil → "Todos os Meus Contatos".

---

## 4. Conectar o Google Contacts

### Passo a passo: autorização OAuth

**No TrueContact:**

1. Abra o **Assistente de Configuração** (na primeira abertura) ou vá a **Configurações → Google Contacts**
2. Clique em **"Conectar Google Contacts"**
3. Uma janela de autenticação do Google será aberta no seu navegador
4. Faça login com a sua conta Google e conceda as permissões solicitadas
5. O TrueContact receberá o token automaticamente e iniciará a sincronização inicial

### O que acontece na primeira conexão?

Quando você conecta o Google Contacts pela primeira vez:

1. O TrueContact lê todos os contatos existentes no Google
2. Todos os contatos locais que ainda não estão no Google são **enfileirados para criação** (propagação total)
3. A sincronização acontece gradualmente (máximo 80 contatos por ciclo) para respeitar os limites da API
4. Um indicador de progresso aparece no cabeçalho do app (badge azul Google)

### Revogar o acesso

Para desconectar o Google Contacts:

1. Vá a [myaccount.google.com/permissions](https://myaccount.google.com/permissions)
2. Localize "TrueContact" na lista
3. Clique em "Revogar acesso"

Isso não apaga os contatos do seu Google Contacts — apenas interrompe a sincronização futura.

---

## 5. Conectar as fontes sociais (LinkedIn, Facebook, Instagram, X, Goodreads, TikTok, Duolingo e PDL)

### Como funciona a fonte Chess.com?

Em Configurações → Fontes → Chess.com, clique em "Conectar Chess.com" e faça login na janela do navegador. Uma vez por dia o TrueContact lê as suas listas — amigos, quem você segue e os pedidos de amizade que você enviou — e cria um contato para cada pessoa que ainda não existe (quem já é contato nunca é duplicado; em "Adicionar como contato" dá para escolher só amigos). Cada perfil é lido pela API pública do Chess.com, sem abrir o navegador: nome, foto, cidade e país (como endereço, só para quem ainda não tem), a data de cadastro no Chess.com, o título de xadrez, a Twitch de quem é streamer, a bio e os links de outras redes da página do perfil. O nome do Chess.com só cria o contato, a foto só preenche quem não tem. Da bio entram só os links; as notas do contato nunca são alteradas.

### Como funciona a fonte Discord?

Desde a 1.0.265. Em Configurações → Fontes → Discord, clique em "Conectar Discord" e faça login na janela do navegador (e-mail e senha, QR pelo app do celular ou login social). Uma vez por dia o TrueContact lê a sua lista de amigos e cria um contato para cada amigo que ainda não existe (quem já é contato nunca é duplicado). Depois, perfil a perfil, com pausa de 20 a 45 segundos entre eles, lê o @, o nome de exibição, a foto, os links da bio e as **contas verificadas de outras redes** que a pessoa ligou ao Discord: GitHub, X, Instagram, TikTok, Facebook, YouTube, Twitch, Reddit, Spotify, Steam, Bluesky, Mastodon, Roblox, Xbox, eBay e PayPal viram perfis sociais do contato, com a URL do próprio serviço; PlayStation, Epic Games, Battle.net, Riot e afins, que não têm página pública, ficam registrados só com o @; um domínio próprio vira site e o Skype vira mensageiro. Essas contas também servem para reconhecer um contato que você já tinha por outra rede. "Amigos desde" entra como data do contato. O nome do Discord só é usado para criar o contato (costuma ser apelido), e a foto só preenche quem ainda não tem foto. O nome de exibição vai para o apelido só quando ele está vazio. As notas do contato nunca são alteradas.

### O TikTok deixa de seguir automaticamente quem eu excluo?

Sim, se você quiser. Ao excluir um contato **sem grupo** que **veio do TikTok** e que você segue, o TrueContact agenda o unfollow. Ele é feito **na sua própria lista "Seguindo"**, sem visitar o perfil de ninguém, porque visitar perfis é o que dispara o captcha. A lista é lida uma vez por sessão, e cada alvo encontrado recebe o clique, com pausa de 8 a 20 segundos entre um e outro.

Limites, os dois em **Configurações → Fontes → TikTok**: "Unfollows por ciclo" (padrão 10) e "Unfollows por dia" (padrão 100). Quem não coube hoje fica para amanhã, e uma sessão que terminou no meio da lista retoma de onde parou. Restaurar o contato da lixeira cancela o unfollow pendente. Quem passou por esse processo nunca mais é recriado pela lista "Seguindo".

A sessão do botão **Resolver captcha na tela virtual** também faz os unfollows pendentes, com você presente para resolver um captcha se ele aparecer.

### Por que o TikTok abre o navegador só duas vezes por dia?

Porque cada abertura do navegador automatizado é exposição ao anti-robô do TikTok. O limite fica em **Configurações → Fontes → TikTok → Sessões por dia** (padrão 2). Esgotado, o selo do TikTok no topo continua mostrando a fila, mas o ciclo registra "2 of 2 browser session(s) used today" e espera a meia-noite. O botão Resolver captcha e o Enriquecer manual não contam.

Outras proteções: pausa crescente depois de um bloqueio (24 horas no primeiro em 7 dias, 72 no segundo, 7 dias do terceiro em diante; o Resolver captcha libera na hora); captcha só conta quando o desafio está visível de verdade, porque o TikTok monta um contêiner vazio depois de cada clique; e o ciclo não abre o TikTok enquanto a sessão do Resolver captcha estiver usando o mesmo navegador.

A recomendação continua sendo manter **Visitar perfis automaticamente** desligado: todos os captchas registrados vieram de visitas a perfil, nenhum da leitura da lista, e a lista "Seguindo" já cria os contatos sem navegador.

### O X estava criando contatos de perfis que eu não sigo. Foi corrigido?

Sim, na 1.0.248. A página "Seguindo" do X também devolve as sugestões "Quem seguir", e o TrueContact aceitava todo perfil que a página trazia. Agora só entra quem o X confirma como seguido (ou seguidor, na lista de seguidores). Perfis criados antes dessa correção a partir de sugestões podem ser excluídos normalmente.

### Amigos Próximos do Instagram: como o TrueContact sabe quem está na lista?

Lendo a lista como ela aparece na tela de Amigos Próximos do próprio Instagram, linha a linha: o controle marcado tem um ícone diferente do vazio, e é por ele que o TrueContact decide. Os dados brutos da página não servem: eles misturam a folha de compartilhar e a bandeja de stories, e por isso, até a 1.0.249, contatos como Netflix Brasil ou ClickBus entravam como amigos próximos sem estar na lista. Se a tela mudar e nenhum marcador for reconhecido, o TrueContact não enfileira ninguém e salva o HTML para diagnóstico, em vez de adivinhar.

### O LinkedIn leu o perfil pela metade. Perco os dados?

Não. Se empresa e cargo, a foto ou uma das listas (telefones, e-mails, sites, endereço) não foi lida por lentidão da página, o perfil é salvo com o que foi lido, **nada do que já existia é apagado**, e o item volta para a fila. O próximo ciclo tenta completar, e na terceira vez aceita o que tiver. O histórico mostra a leitura como "Partial read, retrying next cycle" em vez de erro.

O LinkedIn mudou o layout em outubro de 2026 (o nome saiu do título da página), e o TrueContact passou a ler o nome pelo título da aba. Se o mesmo campo deixar de ser lido em três perfis seguidos, o log avisa que o layout provavelmente mudou de novo.

### Uma página comercial pode transformar meu contato em empresa?

Não mais. X, Facebook e Instagram só marcam como empresa o contato que **eles mesmos criaram**, e nunca desmarcam. A marca de empresa de um contato existente é sua (botão Empresa/Pessoa na ficha), do iCloud ou de uma URL de empresa do LinkedIn, e um perfil pessoal do LinkedIn (`/in/`) sempre prevalece: a pessoa continua pessoa mesmo com a página da empresa junto. A empresa de uma página vai para o campo organização, nunca para o nome. Um contato marcado como empresa fica só com a organização, sem nome de pessoa.

### Quais ajustes de desempenho existem para um servidor Linux (Raspberry Pi)?

Em **Configurações → Geral → Desempenho no servidor Linux**, todos desligados por padrão e sem efeito no Mac e no Windows:

- **Um processo por aba no navegador das redes**: uma aba do LinkedIn chegava a 9 processos por causa de anúncios; com a chave, um só. Há uma chave separada para o LinkedIn.
- **Páginas leves**: vídeo bloqueado no próprio navegador, com cache ligado. O TikTok fica fora, porque um site de vídeo sem vídeo denuncia o robô.
- **Página parada nas pausas entre perfis**: os scripts da página ficam parados durante as pausas de 30 a 90 segundos. O LinkedIn fica fora.
- **Semáforo entre aplicações** ao abrir o navegador, para não disputar CPU com outros bots da mesma máquina.

O resumo de consumo fica em `/api/diagnostico/consumo` (CPU e memória por categoria, duração de cada etapa do ciclo, lançamentos do navegador), e a memória da API é protegida dentro do serviço: o painel não trava mais quando o ciclo encosta no teto de memória.

### Por que os contatos do TikTok vêm só com nome, @ e foto?

O TikTok pede um captcha a cada um ou dois perfis abertos automaticamente — visitar os mais de dois mil perfis que você segue levaria meses. Por isso o TrueContact cria os contatos **direto da lista "Seguindo"**, que já traz o nome, o @usuário e a foto de cada pessoa, sem abrir perfil nenhum (e sem captcha). A bio e os links da bio, que só aparecem no perfil, podem ser buscados para um contato específico pelo botão **Enriquecer** no cartão do TikTok.


### O que significam o ⚠️ e o 🚨 nos selos de fila do topo?

- **⚠️** — a fonte não está conectada: a fila acumula, mas nada é processado até você conectar a conta em **Configurações → Fontes**.
- **🚨** — a fonte precisa de ação sua: a sessão foi perdida ou a rede pediu um **captcha** / bloqueou temporariamente e a fonte está pausada. Passe o mouse sobre o 🚨 para ver o motivo e até quando vai a pausa; clique no selo para abrir a aba da fonte e usar **Conectar** ou **Resolver captcha na tela virtual**. O selo aparece mesmo quando a fila está vazia.

### Acabei de conectar uma fonte e a fila dela está enorme. É normal?

É. Na primeira conexão, o TrueContact lê a lista inteira (amigos, quem você segue) e
coloca na fila todo mundo que ainda não é contato — centenas de perfis de uma vez. Essa
**carga inicial** acontece uma única vez por fonte. A fila anda um pouco a cada ciclo
(as fontes se revezam e cada uma tem uma fatia de tempo, para nenhuma ficar parada) e,
depois de esvaziar, só entram os perfis novos do dia. O mesmo vale para o envio ao
iCloud e ao Google: quando muitos contatos mudam de uma vez, o envio é feito em lotes
para respeitar os limites da Apple e do Google, e os números do cabeçalho caem ao longo
de algumas horas.

### O que é o People Data Labs (PDL) e para que serve?

O PDL é um serviço que **descobre perfis** — principalmente o LinkedIn — a partir de um
telefone ou e-mail. O TrueContact o usa só para contatos que **não têm nenhuma rede
social**: todo dia consulta alguns deles (3 por padrão) e, quando encontra, grava o
perfil e as outras fontes passam a enriquecer o contato normalmente. Cada contato é
consultado uma vez só (e de novo apenas depois de meses), porque cada consulta gasta
crédito. Para ativar, crie uma chave gratuita em
[dashboard.peopledatalabs.com](https://dashboard.peopledatalabs.com/api-keys) (o plano
gratuito dá cerca de 100 consultas por mês) e cole em **Configurações → Fontes → PDL**.
No cartão de um contato, o botão **Descobrir via PDL** faz a consulta na hora.

### Como conectar o Duolingo e o que ele traz

Em **Configurações → Fontes → Duolingo**, clique em **Conectar Duolingo** e entre na
janela que abre (e-mail/senha ou login social). De cada contato, o TrueContact traz
**nome, o perfil** (`duolingo.com/profile/...`) e a **data de entrada** ("Por aqui
desde"), que vira o evento "Duolingo". A **foto só é usada quando é um upload real E o
contato ainda não tem nenhuma** — os avatares de desenho do Duolingo nunca substituem
uma foto verdadeira. Com *Adicionar como contato* ligado, quem você segue (ou só os
mútuos) vira contato novo — **inclusive quem usa só o primeiro nome** (no Duolingo isso é
comum; você decide depois se faz merge ou exclui) — e ninguém é duplicado.

### O TikTok ficou "pausado" por captcha. O que fazer?

O TikTok é a fonte mais desconfiada: de tempos em tempos ele mostra um quebra-cabeça
("arraste a peça para encaixar") no seu próprio perfil, e enquanto ele não é resolvido
nenhum clique funciona — a varredura de quem você segue nem chega a abrir a lista. Quando
isso acontece, o TrueContact **pausa o TikTok** e mostra o motivo em **Configurações →
Fontes → TikTok**, com o botão **Resolver captcha na tela virtual**. Clique nele: a tela
virtual aparece logo abaixo, na própria aba, com o navegador já logado no seu perfil;
resolva o quebra-cabeça
e, assim que o modal some, a pausa é levantada e **a leitura de quem você segue acontece
na hora, nessa mesma janela** (deixe-a aberta; leva alguns minutos). É de propósito: abrir
outra sessão automatizada logo depois faz o TikTok pedir o captcha de novo. Não é preciso
desconectar nem fazer login de novo.

### Como conectar o TikTok e o que ele traz

Em **Configurações → Fontes → TikTok**, clique em **Conectar TikTok** e faça o login na
janela que abre (resolva o captcha, se aparecer). Do perfil de cada contato, o TrueContact
traz **nome, foto e o link da bio** — o TikTok não expõe aniversário, cidade nem data de
cadastro publicamente.

- **Adicionar como contato:** pode criar contatos de *quem você segue* ou só dos *mútuos*
  (quem você segue e te segue de volta). A primeira varredura lê a lista inteira; as
  diárias param cedo assim que só encontram perfis já conhecidos.
- Perfis **só com o primeiro nome ou apelido também entram** (você decide depois se faz merge ou exclui) e quem já é contato nunca é duplicado.
- Como o TikTok é agressivo contra automação, há **carência de 24 horas** após o login e
  pausa automática ao menor sinal de captcha ou limitação.

### O TrueContact consulta o Gravatar dos meus contatos?

Sim. Pelo e-mail de cada contato, o TrueContact verifica se existe um perfil público no
**Gravatar**. Quando existe, acrescenta o nome de usuário do Gravatar, as redes que a pessoa
verificou lá (X, LinkedIn, GitHub, YouTube…) e a foto — **a foto só entra em contatos que ainda
não têm foto**. Cerca de 1 em cada 10 e-mails tem perfil. Ajuste em **Configurações → Fontes →
Gravatar** (ligar/desligar, e-mails por ciclo e de quanto em quanto tempo consultar de novo).

### O que o TrueContact faz com Linktree, about.me e cartões digitais nos meus contatos?

Quando um contato tem como site uma página de links — **Linktree, about.me, bio.site, taplink** ou
um cartão digital como **taggo.one** e **meucontato.io** — o TrueContact lê essa página pública e
acrescenta ao contato as redes sociais, o WhatsApp e o e-mail que a pessoa colocou lá. Nada que
você já tinha é substituído, e tudo fica no histórico como "Agregador de links". Ajuste em
**Configurações → Fontes → Agregadores de links** (ligar/desligar, páginas por ciclo e de quanto em
quanto tempo reler). Links do WhatsApp (wa.me) e do Telegram (t.me) gravados como site viram
automaticamente telefone e perfil do Telegram.

### Como conectar o Goodreads e o que ele traz

O Goodreads é a fonte mais recente. Em **Configurações → Fontes → Goodreads**, clique em
**Conectar Goodreads** e faça o login na janela do navegador que abre (e-mail/senha ou via
Amazon). A sessão fica guardada localmente, como nas outras fontes.

Do perfil de cada contato, o TrueContact traz **nome, foto, site pessoal, cidade,
aniversário** (quando o perfil o torna público) e a **data de entrada no Goodreads**, que
aparece nos eventos do contato como "Goodreads" — do mesmo jeito que a data de conexão do
LinkedIn.

- **Endereço personalizado do perfil:** quando a pessoa criou um endereço próprio no Goodreads
  (ex.: `goodreads.com/luanamasoni`), é ele que fica no contato, no lugar do endereço genérico
  com número (`goodreads.com/user/show/132179255-lua`). Esse nome de usuário ajuda a achar
  duplicados: um perfil "Lua" com o endereço `luanamasoni` aparece nas sugestões de merge
  junto da "Luana Masoni" que você já tinha no iPhone. Os perfis já salvos são lidos de novo
  aos poucos, a cada ciclo, para trocar o endereço.
- **Amigos e quem sigo como contatos:** com as opções *Adicionar amigos como contatos* e
  *Adicionar quem sigo como contatos* ligadas (padrão), a lista de amigos e a de leitores
  que você segue ("People You're Following") são varridas uma vez por dia e quem ainda não
  é contato vira contato novo. Autores seguidos ficam de fora; perfis **só com o primeiro nome
  também entram** (você decide depois no merge) e quem já é contato nunca é duplicado — contatos parecidos entram nas
  sugestões de merge normais. Solicitações de amizade pendentes entram automaticamente
  quando a pessoa aceita.
- **Reverificação:** cada perfil é reconferido a cada 365 dias (ajustável), e o botão de
  enriquecimento no painel do contato visita o perfil na hora.
- **Perfis privados** são respeitados: o TrueContact lê só o que o perfil mostra.

### De quantos em quantos dias cada fonte é reconferida?

Cada fonte tem o seu próprio intervalo, ajustável na aba dela em **Configurações**:

| Fonte | Padrão | Onde ajustar |
|---|---|---|
| LinkedIn | 365 dias | Fontes → LinkedIn |
| Facebook | 7 dias | Fontes → Facebook |
| Instagram | 180 dias | Fontes → Instagram |
| X (Twitter) | 180 dias | Fontes → X |
| Goodreads | 365 dias | Fontes → Goodreads |
| TikTok | 180 dias | Fontes → TikTok |
| Duolingo | 180 dias | Fontes → Duolingo |
| WhatsApp | 30 dias | Fontes → WhatsApp |

O contador reinicia a cada enriquecimento, manual ou automático — reduzir o intervalo deixa
os dados mais frescos, mas aumenta o volume de visitas e, com ele, o risco de a rede limitar
a conta. Os limites por ciclo de cada aba continuam valendo em cima disso.

### Como conectar o Instagram e o X (Twitter)

O fluxo é o mesmo do LinkedIn e do Facebook: em **Configurações → Fontes**, clique em
**Conectar Instagram** ou **Conectar X**, faça o login na janela do navegador que abre
(no servidor sem tela, pela tela virtual embutida na própria página) e pronto — a sessão
fica guardada localmente.

- **Carência de 24 horas:** após um login novo, as leituras só começam no dia seguinte,
  para a conta não levantar suspeita.
- **Pausa automática:** ao menor sinal de bloqueio ou limitação, a rede entra em pausa e
  tenta de novo mais tarde, sozinha.
- **Adicionar como contato:** o Instagram pode criar contatos de *quem você segue*, dos
  *mútuos* ou dos *Amigos Próximos*; o X, de quem você segue. Perfis só com o primeiro nome
  também entram (você decide depois no merge) e quem já é contato nunca é duplicado.

As duas redes são **fontes de enriquecimento**: o TrueContact lê perfis públicos para preencher os seus contatos, mas nunca publica, comenta ou envia nada em seu nome.

### Instalei em um servidor Linux sem tela (Raspberry Pi, Homebridge). Como conecto o LinkedIn e o Facebook?

O login acontece **no próprio servidor**, numa tela virtual que o instalador monta para isso — e você a acessa do seu computador como se estivesse controlando outro à distância:

1. Na interface web do servidor (ex.: `http://IP-DO-SERVIDOR:6969`) → **Configurações** → seção **LinkedIn** ou **Facebook**, clique em **Reconectar** (ou **Conectar**)
2. A tela de login do servidor **aparece ali mesmo, embaixo do botão**, já conectada. Não é preciso terminal, senha nem outro aplicativo
3. Faça o login normalmente — verificação em duas etapas, captcha, o que aparecer. Você tem **10 minutos**
4. Assim que a rede confirmar a sessão, o TrueContact a salva, fecha o navegador e o bloco passa a **Conectado**

Se preferir, a mesma tela pode ser aberta em outra aba (link ao lado do título) ou por qualquer cliente VNC no endereço mostrado abaixo dela.

**Por que não copiar os cookies do meu navegador?** O LinkedIn e o Facebook amarram a sessão ao navegador e ao dispositivo em que o login foi feito. Uma sessão copiada — pela extensão Cookie-Editor ou pelo arquivo `auth.json` do app de desktop — é reconhecida como **sequestro de sessão**: a rede a revoga no servidor e derruba também o navegador de origem (você é deslogado no seu computador). Foi assim em testes reais. Por isso a sessão precisa **nascer** no navegador do servidor. Por isso a tela não oferece mais importação de sessão por arquivo ou colagem.

A tela virtual fica sempre ligada: além do login, a própria raspagem passa a rodar com janela nela, o que reduz os sinais de automação que essas redes procuram. O acesso à tela (VNC na porta 5900, noVNC na 6080) tem senha; em redes que não sejam totalmente confiáveis, restrinja com firewall ou use um túnel SSH.

**Importante:** não deixe o app do Mac e o servidor rodando ao mesmo tempo com as mesmas contas — dois hubs sincronizando a mesma agenda do iCloud/Google geram conflitos, e duas máquinas raspando o LinkedIn com a mesma sessão podem fazer a rede derrubá-la.

### Como conectar

Para qualquer uma das duas, o processo é o mesmo:

1. Abra as **Configurações** e vá à seção **LinkedIn** ou **Facebook**
2. Clique em **"Conectar"**
3. Uma janela de navegador se abre na página de login da rede
4. Faça login normalmente, incluindo a verificação em duas etapas, se houver
5. Assim que a rede confirmar a sessão, a janela fecha e o TrueContact assume dali em diante

A sessão fica salva localmente, como acontece no seu próprio navegador. Se a rede encerrar a sessão — troca de senha, logout remoto, inatividade — o app avisa nas Configurações e basta reconectar.

### O que cada radar faz

| Radar | LinkedIn | Facebook |
|---|---|---|
| Novos contatos | Novas conexões entram na fila de enriquecimento | Novos amigos e solicitações pendentes entram na fila |
| Aniversários | Sim | Sim |
| Mudança de cargo/emprego | Sim | Sim |
| Convites/solicitações | Convites pendentes aparecem no painel inicial | Solicitações enviadas são priorizadas na fila |
| Data de início | Data da conexão | Data de amizade |

### Ritmo e risco de bloqueio

Tanto o LinkedIn quanto o Facebook são agressivos contra automação. O TrueContact trabalha devagar de propósito:

- **Limite por ciclo** — quantos perfis são visitados a cada execução. O recomendado para o Facebook é **1 a 5**; acima disso o risco de bloqueio temporário cresce bastante
- **Intervalo de reverificação** — de quantos em quantos dias o perfil de cada contato é revisitado. O contador reinicia após qualquer enriquecimento, manual ou automático
- **Uma varredura de lista por dia** — a lista de amigos e a de conexões são varridas no máximo uma vez a cada 24 horas

Se o TrueContact detectar um bloqueio ou limitação de taxa, ele **encerra a sessão sozinha** e mostra um aviso nas Configurações, em vez de insistir e agravar a situação.

### Casos especiais que o sistema reconhece

- **Páginas de empresa** — perfis que são páginas comerciais são marcados como empresa, e não como pessoa
- **Perfis memorializados** — perfis de pessoas falecidas são detectados e removidos da fila de raspagem após o processamento
- **Perfis apagados** — quando um endereço deixa de existir (erro 404), o perfil é marcado como inativo em vez de ser tentado indefinidamente

### Enriquecer um contato manualmente

Não precisa esperar o ciclo automático. No painel do contato, o botão de enriquecimento ao lado do perfil social visita aquele perfil na hora e traz o que encontrar.

---

## 6. Conectar o WhatsApp e o Telegram

### Como conectar o Telegram e o que ele traz

O Telegram usa a API oficial de clientes (MTProto) — sem navegador. Antes de conectar,
crie um app em **my.telegram.org → API development tools** e cole o `api_id` e o
`api_hash` em **Configurações → Fontes → Telegram** (eles identificam o aplicativo, não
a sua conta, e ficam salvos só no seu servidor). Depois clique em **Conectar Telegram**
e escaneie o QR code com o app oficial (Configurações → Dispositivos → Conectar
dispositivo). Contas com verificação em duas etapas digitam a senha na própria tela.

Dos seus contatos do Telegram, o TrueContact traz **nome, foto, aniversário** (quando a
pessoa o configurou e a privacidade permite), **e-mails da bio** e o **perfil do
Telegram como rede social com link**: `t.me/<usuario>` quando a pessoa tem @usuário, ou
o link oficial pelo número, `t.me/+<número>`, quando não tem. Esse link vai para o
iPhone (perfil social "Telegram") e para o Google (site com rótulo "telegram"). A
primeira sincronização começa sozinha logo depois de conectar; as seguintes rodam em todo
ciclo. Quem está na sua agenda do Telegram e ainda não é contato vira contato novo,
mesmo com nome de uma palavra só. O casamento é por telefone, com as mesmas regras
de sempre: procurar antes de criar, enriquecer sem sobrescrever, propagar ao
iCloud/Google. Com a opção de verificação ligada, o TrueContact também confere em lotes
pequenos **quais telefones da sua agenda têm Telegram** (a importação de teste é
desfeita na hora, sem poluir sua agenda do Telegram).

### Passo a passo: leitura do QR Code (WhatsApp)

**No TrueContact:**

1. Abra as **Configurações** (ícone de engrenagem no canto superior direito)
2. Vá à seção **WhatsApp**
3. Clique em **"Conectar WhatsApp"**
4. Um **QR Code** aparecerá na tela — você tem 60 segundos para lê-lo

**No seu celular (iOS ou Android):**

1. Abra o **WhatsApp**
2. Vá a **Configurações → Dispositivos conectados**
3. Toque em **"Conectar um dispositivo"**
4. Aponte a câmera para o QR Code na tela do computador
5. Aguarde a confirmação

> **Nota:** O TrueContact aparece como "Chrome em [nome do computador]" na lista de dispositivos conectados. O WhatsApp permite até 4 dispositivos ao mesmo tempo.

### Resolver problemas de conexão

**O QR Code expira antes de conseguir ler:**
Clique em "Atualizar QR Code" nas Configurações. O código é regenerado instantaneamente.

**"Sessão desligada" aparece nas Configurações:**
O WhatsApp desconecta dispositivos inativos por mais de 14 dias. Repita o processo de conexão.

**O WhatsApp diz "Número de dispositivos atingido":**
Remova um dispositivo existente em **WhatsApp → Configurações → Dispositivos conectados** e tente novamente.

### O que o TrueContact importa do WhatsApp

Ao conectar, o TrueContact percorre as suas conversas e usa o que encontra para enriquecer os contatos que já existem — foto de perfil, nome de exibição e, em contas comerciais, os dados do perfil Business (site, e-mail, endereço, categoria).

Quando chega uma mensagem de um número que não está na sua base, um contato novo é criado com esse telefone. Antes de criar, o sistema procura o número entre os contatos existentes, incluindo a variação com e sem o nono dígito — o objetivo é enriquecer quem já existe, não gerar duplicados.

> **Nunca são criados contatos anônimos.** Se o WhatsApp não fornecer nenhum nome para o número, o contato não é criado — um registro só com um telefone e sem nome só ia sujar a sua agenda.

### Por que alguns contatos aparecem sem foto mesmo com WhatsApp?

Veja [Por que não vejo a foto de alguns contatos do WhatsApp?](#por-que-não-vejo-a-foto-de-alguns-contatos-do-whatsapp) na seção de sincronização — é uma configuração de privacidade do outro lado, não uma falha do app.

---

## 7. Templates e Automações

### O que são templates?

Os **templates** são mensagens pré-configuradas que o TrueContact envia automaticamente em determinados eventos — principalmente aniversários. Você pode criar múltiplos templates para o mesmo evento, e o sistema sorteia qual usar, tornando as mensagens mais naturais e variadas.

### Criar uma mensagem de aniversário

1. Abra as **Configurações**
2. Vá à seção **Templates de Aniversário**
3. Clique em **"Adicionar Template"**
4. Escreva a mensagem, usando a variável `{{nome_amigavel}}` para personalizar
5. Clique em **"Salvar"**

**Exemplo:**
```
Olá {{nome_amigavel}}! 🎂 Hoje é o seu dia especial — muitas felicidades e que este novo ano traga tudo o que merece! 🥳
```

### A variável `{{nome_amigavel}}`

A variável é substituída pelo nome mais natural do contato, seguindo esta ordem de prioridade:

1. **Apelido (Nickname)** — se definido no iCloud (ex: `Zé`)
2. **Primeiro nome** — se não tiver apelido (ex: `José`)
3. **Nome completo** — apenas como último recurso

> **Dica:** Para adicionar um apelido no iPhone, abra o contato → "Editar" → "adicionar campo" → "Apelido".

### Sorteio de mensagens e delay de digitação

**1. Sorteio aleatório:**  
Quando há múltiplos templates, o sistema escolhe um aleatoriamente. O mesmo contato receberá uma mensagem diferente a cada aniversário.

**2. Delay de digitação (simulação humana):**  
Antes de enviar, o TrueContact ativa o indicador "digitando..." no WhatsApp e aguarda um tempo proporcional ao comprimento da mensagem. Isso reduz significativamente a probabilidade de as mensagens serem marcadas como spam.

> **Aviso:** Não configure templates com linguagem de marketing ou links promocionais. Os templates devem ser mensagens genuínas e pessoais.

### A que horas os parabéns são enviados?

O envio abre no horário que você definir (por padrão, **09:00**) e **fecha às 17:00**. Uma mensagem de parabéns que chega às 22:00 já não é simpática, então, passado o limite, o sistema não envia mais naquele dia — nem mesmo as retentativas de mensagens que falharam.

Se uma mensagem falhar dentro da janela — WhatsApp momentaneamente desconectado, por exemplo — ela é tentada novamente de forma automática, ainda no mesmo dia.

Os dois horários ficam em **Configurações → Templates de Aniversário**.

### Enviar na hora ou agendar

Além do envio automático de aniversário, você pode falar com um contato a partir do próprio painel dele. No card de telefones, ao lado do número:

- **Enviar agora** — abre o campo de mensagem e envia na hora
- **Agendar** — escolhe data e hora para a mensagem sair sozinha

O agendamento aceita **texto, imagem, áudio, vídeo e documento**. Mensagens agendadas podem ser editadas — tanto o conteúdo quanto a data — enquanto não tiverem saído, e todas aparecem no histórico do contato depois de enviadas.

### O card de aniversário no painel

No painel inicial, o card **Aniversariantes de Hoje** mostra, ao lado de cada pessoa, o mesmo botão de parabéns que existe dentro do contato: **🎂 Parabéns** enquanto a mensagem não saiu, **✅ Enviado** depois. Assim dá para percorrer a lista do dia sem abrir contato por contato. Quem não tem telefone cadastrado continua mostrando a data.

---

## 8. Operações em Lote e Indicadores

### Que pistas novas a tela de sugestões de merge usa?

A tela pontua cada par de 0 a 100 e mostra as pistas que encontrou. Pistas acrescentadas em outubro de 2026:

- **Só um tem grupo** (+20): você agrupa quem conhece, e o contato sem grupo costuma ser a cópia que uma rede criou depois. O contrário, **os dois têm grupo** (−15), é pista contra.
- **@ é o nome abreviado em ordem** ("Cristiane" @crisluzsa = Cristiane Luz Salustiano) e **@ é a inicial do nome + um sobrenome raro** ("Dan" @dfamano = Daniel Famano).
- **@ é o nome sem a letra acentuada** (Tércio Gaspar × @trciogaspar).
- **E-mail sem o sufixo curto é o @** ("fabriciovmartins.sp" × @fabriciovmartins), **primeiro nome + iniciais + sobrenome** ("julioaoliveira") e **nome invertido** ("santosigor").
- **Nome ou @ colado** com o início do primeiro nome e um sobrenome raro ("Gusjahnz" × Gustavo Jahnz).

Essas pistas só alimentam a sugestão manual. O merge automático continua restrito aos casos da seção **Configurações → Normalização → Deduplicação e Merge**, cada um com o seu interruptor. Um contato cujo nome é só "User" ou o próprio @ não gera sugestão por nome.

### Como filtrar as sugestões por pista?

No topo da lista de sugestões há filtros **Com / Sem** para cada pista, com a contagem de pares, no mesmo estilo dos filtros de fonte da lista de contatos. O filtro vale sobre a lista inteira de pares calculados, não só sobre os primeiros mil exibidos. O botão de merge na ficha do contato é um link: Command ou Ctrl + clique abre a comparação em outra aba.

### Fiz merge e o par continuou na lista. Foi corrigido?

Sim. O recálculo das sugestões roda em segundo plano e pode esperar o ciclo de leitura terminar. Até a 1.0.253, nesse intervalo o par recém-fundido continuava na tela e um segundo clique dava erro. Agora fundir, excluir ou ignorar tira o par da lista na hora, e a lista é podada a cada 15 segundos de pares com contato na lixeira.

### O merge pode misturar o nome de dois contatos?

Não mais. O nome do contato vencedor é mantido como um bloco: primeiro nome, nome do meio e sobrenome vêm do mesmo contato. Até a 1.0.258 o merge automático pegava cada campo do primeiro contato que o tinha preenchido, e "Heitor Kuser" virou "Heitor Kuser Mercado Imobiliário Kuser" ao absorver um contato criado pelo Instagram. O vencedor é o contato que está no iCloud e, entre dois, o mais antigo; um contato com nome genérico ("User") nunca vence.

### Como funciona o cartão "Sem grupo" da tela inicial?

Ele abre em **Outras**, escondendo os contatos criados pelas listas do TikTok, Duolingo e Goodreads, que costumam ser muitos. O filtro por origem mostra cada rede com a contagem, e inclui o Telegram. Cada linha traz o chip da rede de onde o contato veio, o botão de grupo e um botão de excluir. Atribuir um grupo tira o contato da lista na hora. No celular, aniversariantes, contatos sem grupo e convites do LinkedIn ficam numa faixa no topo da lista, e cada um abre o cartão em tela cheia.

### O merge junta os nomes dos dois contatos?

Sim, quando um nome acrescenta algo ao outro. No comparador do **Merge Inteligente**, logo abaixo da linha **Nome**, aparece a linha **Nome combinado** já marcada — por exemplo, "Andressa Maltaca" com "Andressa Gonçalves" vira **Andressa Gonçalves Maltaca**. A junção usa a mesma higienização de nomes do restante do app: não repete partes, ignora diminutivos ("Dan" dentro de "Daniel") e preserva conectivos quando um nome já contém o outro ("Priscilla Freitas" com "Priscilla Bilecki de Freitas" fica "Priscilla Bilecki de Freitas"). As partes novas entram antes do último sobrenome do nome que você escolheu na linha Nome, para o contato continuar sendo conhecido pelo mesmo sobrenome. Desmarque a caixa para gravar só o nome escolhido.

### Como o TrueContact decide a confiança de uma sugestão de merge?

Cada sugestão da tela **Merge Inteligente** recebe uma **pontuação de 0 a 100** e uma faixa: **Alta** (75 ou mais), **Média** (40 a 74) ou **Baixa**. A pontuação soma as pistas encontradas, que aparecem como etiquetas abaixo do par:

- **mesmo e-mail / mesmo telefone** — identificador forte, sempre 100.
- **nome completo idêntico**, **nome e sobrenome iguais**, **nome parcial** ("Vitor Celestino" dentro de "Vitor de Oliveira Celestino") ou só **mesmo primeiro nome**.
- **@usuário em outra rede** — o mesmo nome de usuário em redes diferentes (ex.: `@espeiorin` no Duolingo e no LinkedIn). É a pista mais forte depois de e-mail e telefone.
- **e-mail de um é o @usuário do outro** — `abeloliveiraj@gmail.com` num contato e o Duolingo `@abeloliveiraj` em outro viram sugestão mesmo com nomes diferentes. E-mails genéricos (`contato@`, `info@`) e os que começam por um primeiro nome comum (`ricardo@`) não contam.
- **Telegram do mesmo telefone** — quando o Telegram de um contato foi achado pelo número e esse número está no telefone de outro contato, é a mesma pessoa (nota 100).
- **mesmo @usuário com nomes diferentes** — o par é sugerido mesmo quando os nomes não batem: "Alexandre" (Duolingo `@fracazo`) com "Alex Fracazo" (LinkedIn `@fracazo`), ou "Doug" com "Douglas Etges" (`@douglasetges`). Um primeiro nome compatível ("Alex" ≈ "Alexandre") soma; um primeiro nome sem relação pesa contra. Handles que são só o primeiro nome, só dígitos ou lixo de página não contam.
- **@usuário tem o sobrenome** ou **@usuário é o nome** (`@marlonmoser` para Marlon Moser).
- **sobrenome raro** — "Renan Saad" com "Renan Cararo Saad" pesa muito mais que "Bruno Oliveira" com "Bruno Nascimento de Oliveira": a pontuação conta quantos contatos da sua base têm aquele sobrenome.
- **primeiro nome raro** — o mesmo vale para o primeiro nome: "Priscilla Freitas" com "Priscilla Bilecki de Freitas" sobe para Alta porque só há três Priscillas na base, enquanto "Rodrigo" não ajuda em nada.
- **nome idêntico de uma palavra** — "Rodrigo" com "Rodrigo", sem sobrenome dos dois lados, vale quase nada (15) e fica na faixa Baixa, salvo outra pista.
- **nome do meio diferente** — pista negativa: "Felipe Augusto Gomes" e "Felipe Cohen Gomes" têm o mesmo primeiro e último nome, mas o meio contradiz. Iniciais contam como compatíveis ("Augusto C. Ligeiro" = "Augusto César Ligeiro").
- **@usuário é o próprio nome** (`@renansaad`) — handle de nome real, não apelido: pequeno reforço.
- **mesma empresa**, **mesmo aniversário**, **mesmo cargo** e **mesmo domínio** (site ou e-mail corporativo, ex.: `@roberthalf.com.br`).
- **mesma cidade** — só pesa em cidades pouco comuns na sua base: em Curitiba ou São Paulo, onde está boa parte da rede, morar na mesma cidade não diz nada.
- **pistas contra** — empresas diferentes, aniversários diferentes, cidades diferentes ou telefones de DDD diferente baixam a nota. Foram medidas com o seu próprio histórico: aparecem em boa parte dos pares que você ignorou e quase nunca nos que você fundiu.
- **abrir o contato** — no comparador, o nome de cada contato no topo abre a ficha dele no TrueContact numa nova aba, sem perder o merge em andamento (no app desktop, abre na mesma janela).
- **1 de N candidatos** — pista negativa: um contato só com o primeiro nome ("Andre") que combina com dezenas de Andrés perde pontos; **único com pista entre N** é o contrário, quando só um dos candidatos tem alguma pista real.

Dois contatos com **@usuário diferente na mesma rede** nunca são sugeridos: são pessoas diferentes.

Por padrão a lista mostra só as faixas Alta e Média, ordenadas pela pontuação. O link **Mostrar N de baixa confiança** revela o resto. Contatos de uma só palavra que combinam com vários candidatos aparecem **agrupados**: um cartão com o contato e a lista de candidatos ranqueados, e o botão **Ignorar todos os candidatos** descarta o grupo de uma vez. Confirmar o merge de um candidato remove automaticamente as outras sugestões que envolviam o contato fundido.

O **auto-merge** continua restrito aos casos sem ambiguidade (ver abaixo); a pontuação só orienta a revisão manual.

### Lixeira: recuperar contatos excluídos

Contatos excluídos não são apagados imediatamente — vão para a **Lixeira**, acessível pelo ícone de lixo no cabeçalho.

A Lixeira tem o mesmo formato da tela principal de contatos: a lista fica à esquerda e, ao clicar em um contato, os dados completos aparecem à direita (telefones, e-mails, redes sociais, endereços, datas, notas e grupos). A diferença é que tudo fica em **modo de leitura** — não é possível editar campos, enviar mensagens pelo WhatsApp nem enriquecer o perfil enquanto o contato estiver na lixeira.

Para trazer um contato de volta:

1. Abra a **Lixeira** pelo ícone de lixo no cabeçalho
2. Localize o contato (use a busca, se necessário)
3. Clique em **Restaurar** — no ícone ao lado do contato na lista ou no botão no topo dos detalhes

Ao restaurar, o contato volta à listagem principal e é reenfileirado para sincronização com todos os provedores conectados (iCloud e Google).

Contatos que sumiram por causa de um **merge** aparecem na lixeira com a marcação *"fundido em [nome]"*, indicando em qual contato os dados foram consolidados.

### Esvaziar a lixeira

O botão **Limpar lixeira**, no canto superior direito da tela, apaga permanentemente todos os contatos da lixeira e propaga a exclusão para os provedores conectados. É pedida uma confirmação antes, e **esta ação não pode ser desfeita**.

### Excluir múltiplos contatos de uma vez

Na lista lateral (sidebar), você pode selecionar e excluir vários contatos ao mesmo tempo:

1. Clique no ícone de **seleção múltipla** no topo da sidebar
2. Marque os contatos que deseja excluir (checkbox ao lado de cada nome)
3. Clique em **"Excluir selecionados"**
4. Confirme a exclusão na caixa de diálogo

> **Atenção:** A exclusão enfileira a remoção nos provedores conectados (iCloud e Google). No TrueContact os contatos vão para a **Lixeira** e podem ser restaurados; a exclusão só se torna definitiva ao limpar a lixeira.

### Merge em lote

Também é possível selecionar múltiplos contatos e enviá-los diretamente para o **Merge Inteligente**:

1. Selecione 2 ou mais contatos na sidebar
2. Clique em **"Fazer Merge"**
3. O sistema abre a tela de merge com os contatos pré-selecionados

### O painel inicial

Quando nenhum contato está selecionado, o TrueContact mostra o painel do dia, com três cards:

- **Aniversariantes de Hoje** — quem faz aniversário hoje, com o botão de parabéns direto no card
- **Sem Grupo** — contatos que ainda não foram classificados; o botão *Grupo* atribui um grupo ali mesmo, com os grupos usados recentemente no topo da lista
- **Convite Pendente** — contatos com perfil do LinkedIn mas sem data de conexão, ou seja, convites que provavelmente ainda não foram aceitos. O botão de descartar tira da lista quem você não quer mais ver

### Indicadores de fila no cabeçalho

O cabeçalho do TrueContact mostra badges coloridos indicando contatos aguardando sincronização:

| Badge | Cor | Significado |
|---|---|---|
| Ícone LinkedIn | Azul LinkedIn | Contatos na fila de enriquecimento LinkedIn |
| Ícone Facebook | Azul Facebook | Contatos na fila de enriquecimento Facebook |
| Ícone Instagram, X, Goodreads, TikTok e Duolingo | Cor de cada rede | Perfis na fila de cada uma dessas fontes |
| Ícone WhatsApp | Verde | Números aguardando verificação no WhatsApp |
| Ícone Telegram | Azul Telegram | Números aguardando verificação no Telegram (só aparece quando há fila) |
| Ícone Google | Azul Google | Contatos aguardando sincronização com o Google Contacts |
| Ícone Apple | Cinza | Contatos aguardando sincronização com o iCloud |

Quando há itens em fila, o ícone da respectiva rede anima com um efeito pulsante. Os badges desaparecem quando a fila é processada. Uma fonte **desconectada** aparece com ⚠️ ao lado do logo — a fila dela continua acumulando e será processada quando reconectar. **Clicar em qualquer badge** abre as Configurações direto na aba daquela fonte.

### Como fazer merge pelo celular?

No celular, a tela de merge mostra **um cartão por campo** em vez da tabela: no topo
fica a prévia do contato final (foto, nome, cargo), com a legenda de quem é **A** e quem
é **B**. Toque na opção que quer manter — valores que os dois contatos têm aparecem uma
vez só, com as duas letras. Telefones, e-mails e redes vêm todos marcados (o padrão é
somar tudo); desmarque o que não quiser. Campos iguais nos dois ficam recolhidos em
"N campos iguais". **Ignorar** e **Confirmar Merge** ficam sempre visíveis no rodapé.

### Contatos Duplicados (Merge Inteligente)

O TrueContact detecta automaticamente contatos duplicados comparando:
- Nome (fuzzy matching)
- Email
- Telefone (normalizado)
- Perfis de redes sociais

Quando novos duplicados são detectados, uma **notificação nativa** é enviada com a contagem. Clique na notificação para abrir diretamente a tela de Merge.

Casos sem qualquer ambiguidade — contatos com exatamente o mesmo nome e nenhum dado conflitante entre si — são fundidos automaticamente pelo **auto-merge de alta fidelidade**. Também entram nele contatos com o nome completo idêntico e o mesmo nome de usuário em outra rede (ex.: "Edward Konig" com LinkedIn @edwardkonig e "Edward Konig" com TikTok @edwardkonig), desde que não tenham usuários diferentes numa mesma rede. E entram ainda os de nome completo idêntico quando o primeiro nome e o sobrenome são raros na sua base (ex.: "Estefanie Mosko") e nada entre os dois se contradiz — empresa, aniversário, cidade ou DDD diferentes impedem o merge. O mesmo vale quando o e-mail de um contato é o nome de usuário do outro numa rede (ex.: fagosi777@gmail.com e o TikTok @fagosi777) e os nomes batem. O auto-merge vem ligado por padrão. Em **Configurações → Normalização → Deduplicação e Merge** você pode desligá-lo por inteiro ou regra por regra: cada linha mostra um exemplo e quantos pares ela fundiria agora, e o histórico de cada merge diz qual regra o fez. Todo merge automático fica registrado no histórico e pode ser desfeito.

---

## 9. Histórico e Reversão

### O que é o selo "Novo" ou "Alterado" ao lado da fonte de um campo?

Desde a 1.0.260, cada campo da ficha (e-mails, telefones, redes sociais, sites, endereços, datas, grupos, mensageiros, relacionados, nome, cargo, empresa, apelido, notas e foto) mostra, ao lado do ícone da fonte, um selo **Novo** quando o item foi acrescentado nos últimos 7 dias, ou **Alterado** quando o valor mudou nesse período. Exemplos: um e-mail que não existia e chegou pelo iCloud aparece como "Novo"; um cargo ou empresa que o LinkedIn atualizou aparece como "Alterado". Passe o mouse sobre o selo para ver a origem e a data da mudança. Na lista de contatos, à esquerda, um brilho verde ao lado do nome indica que o contato ganhou campos novos nesse período, e âmbar que só houve alterações. Um contato criado nesse período aparece com um ícone azul de pessoa com "+", que substitui o brilho. Um contato que passou por merge nesse período mostra também um ícone de merge: rosa quando foi manual, um robô verde-azulado quando foi automático. E o mesmo ícone roxo de merge que aparece na ficha indica, na lista, que existe uma sugestão de merge envolvendo o contato. O selo vem do histórico do contato, então vale igual para qualquer fonte. A janela de 7 dias é a chave `novidades_dias` em Configurações.

### Existe uma auditoria do que os provedores removeram?

Sim, desde a 1.0.255. Todo domingo às 04:10 o TrueContact varre o histórico dos últimos 7 dias e lista o que o iCloud ou o Google removeram e **ainda falta** no contato, marcando como suspeito o item que o outro provedor ainda tem. O resultado fica em `/api/diagnostico/perdas`, e cada item suspeito vai para o log do painel com um aviso. Para rodar fora de hora: `POST /api/auditoria/perdas` com `{ "dias": 7 }`. A auditoria roda num processo separado e não trava o painel.

### Por que "Desfazer merge" às vezes é recusado?

Porque o contato absorvido já não está na lixeira: foi excluído em definitivo ou a lixeira foi esvaziada. Sem ele, não há o que restaurar, e o botão responde com o erro "contatos fundidos não estão mais na lixeira" em vez de refazer um merge pela metade. Desfazer merge também passou a remover do vencedor **só o que o merge acrescentou**, comparando o retrato de antes com o de depois.

### As fotos no histórico ocupam muito espaço?

Não mais. Cada registro do histórico guarda só uma referência à foto, e a foto fica uma única vez numa tabela própria. Antes, a foto inteira era copiada em texto dentro de cada registro, em cerca de 3,6 vezes o tamanho original, e o histórico chegou a ocupar metade do banco. Os registros antigos são convertidos aos poucos pelo radar, e as fotos órfãs saem na manutenção das 03:30.

### A linha do tempo de cada contato

Todo contato tem uma aba de **Histórico** que registra tudo o que aconteceu com ele: sincronizações, enriquecimentos, edições manuais, merges, limpezas automáticas e mensagens enviadas pelo WhatsApp.

Cada entrada mostra:

- **Quando** aconteceu, com data e hora
- **De onde veio** — ícone da fonte (Apple, Google, LinkedIn, Facebook, WhatsApp, edição manual, merge ou limpeza automática)
- **O que mudou** — campos acrescentados em verde, removidos em vermelho e alterados com o valor antes e depois

Entradas que não alteraram nada — uma sincronização que apenas confirmou o que já existia — ficam recolhidas por padrão, para que só as mudanças reais chamem atenção. Um botão no topo da aba exibe todas.

### Reverter para um estado anterior

Se um radar sobrescreveu algo que não devia, você não precisa reconstruir o contato à mão:

1. Abra o contato e vá à aba **Histórico**
2. Encontre a entrada imediatamente **anterior** ao problema
3. Clique em **"Reverter para este estado"** e confirme

O contato volta exatamente àquele estado — inclusive campos que tinham sido acrescentados depois são removidos, não apenas os que tinham sido perdidos. A reversão é propagada para o iCloud e o Google como qualquer outra alteração.

### Desfazer um merge

Merges têm um botão próprio: **"Desfazer merge"**. Além de devolver o contato vencedor ao estado anterior, ele **restaura os contatos que tinham sido absorvidos**, com os grupos e relacionamentos que existiam na época.

Isso funciona mesmo quando o vencedor é um contato antigo sem histórico recente: o próprio
registro do merge guarda como ele estava antes. A exceção são merges feitos antes dessa
guarda existir (12/10/2026 ou antes) em contatos cujo histórico já expirou: nesses casos o
desfazer é **parcial** — o duplicado volta da lixeira, o vencedor mantém o que absorveu e o
painel avisa, para você remover à mão o que não quiser.

### Por quanto tempo o histórico é mantido?

A interface mostra as **últimas 100 entradas** de cada contato. No banco, a limpeza das madrugadas apaga os registros com mais de 30 dias, com duas exceções desde a 1.0.255: as **últimas 10 entradas de cada contato ficam sempre**, por mais antigas que sejam, e o **registro de um merge é mantido enquanto o contato absorvido existir**, para que o botão Desfazer merge continue funcionando. Veja também [Quanto espaço o TrueContact ocupa no disco?](#quanto-espaço-o-truecontact-ocupa-no-disco).

---

## 10. Atualizações

### Como funciona a atualização automática

O TrueContact usa um sistema de **atualização OTA (Over-The-Air)** — silencioso, automático e seguro.

**O processo:**

1. Quando o app inicia, verifica discretamente se existe uma versão mais recente
2. Se encontrar uma versão nova, **baixa em segundo plano** sem interromper o seu trabalho
3. Quando o download estiver completo, uma **notificação discreta** pergunta se quer instalar agora ou na próxima abertura
4. A atualização é instalada e o app reinicia automaticamente

**Segurança:**  
Cada arquivo de atualização é **assinado criptograficamente** antes de ser publicado. O TrueContact verifica esta assinatura antes de instalar — se a assinatura não corresponder, a atualização é rejeitada automaticamente.

> **Nota:** As atualizações são publicadas no repositório público `osnipassos/truecontact-releases`. O código-fonte nunca é publicado nesse repositório — apenas os binários compilados e assinados.

### Ver a versão atual

Consulte a versão instalada em **Configurações → Sobre o TrueContact**, no fundo da página.

---

*Última atualização: 23 de outubro de 2026 — versão 1.0.259*  
*[Reportar um problema](https://github.com/osnipassos/truecontact-releases/issues) · [Início](https://osnipassos.github.io/truecontact-releases/)*
