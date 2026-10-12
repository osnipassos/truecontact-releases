# TrueContact — Manual do Usuário

> **Versão do documento:** Agosto 2026  
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
Fontes → TikTok**, com o botão **Resolver captcha na tela virtual**. Clique nele: o
navegador já logado abre no seu perfil na tela virtual (noVNC); resolva o quebra-cabeça
e, assim que o modal some, a pausa é levantada sozinha e a varredura volta no próximo
ciclo. Não é preciso desconectar nem fazer login de novo.

### Como conectar o TikTok e o que ele traz

Em **Configurações → Fontes → TikTok**, clique em **Conectar TikTok** e faça o login na
janela que abre (resolva o captcha, se aparecer). Do perfil de cada contato, o TrueContact
traz **nome, foto e o link da bio** — o TikTok não expõe aniversário, cidade nem data de
cadastro publicamente.

- **Adicionar como contato:** pode criar contatos de *quem você segue* ou só dos *mútuos*
  (quem você segue e te segue de volta). A primeira varredura lê a lista inteira; as
  diárias param cedo assim que só encontram perfis já conhecidos.
- Perfis **sem nome completo são ignorados** e quem já é contato nunca é duplicado.
- Como o TikTok é agressivo contra automação, há **carência de 24 horas** após o login e
  pausa automática ao menor sinal de captcha ou limitação.

### Como conectar o Goodreads e o que ele traz

O Goodreads é a fonte mais recente. Em **Configurações → Fontes → Goodreads**, clique em
**Conectar Goodreads** e faça o login na janela do navegador que abre (e-mail/senha ou via
Amazon). A sessão fica guardada localmente, como nas outras fontes.

Do perfil de cada contato, o TrueContact traz **nome, foto, site pessoal, cidade,
aniversário** (quando o perfil o torna público) e a **data de entrada no Goodreads**, que
aparece nos eventos do contato como "Goodreads" — do mesmo jeito que a data de conexão do
LinkedIn.

- **Amigos e quem sigo como contatos:** com as opções *Adicionar amigos como contatos* e
  *Adicionar quem sigo como contatos* ligadas (padrão), a lista de amigos e a de leitores
  que você segue ("People You're Following") são varridas uma vez por dia e quem ainda não
  é contato vira contato novo. Autores seguidos ficam de fora; perfis **sem nome completo
  são ignorados** e quem já é contato nunca é duplicado — contatos parecidos entram nas
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
  *mútuos* ou dos *Amigos Próximos*; o X, de quem você segue. Perfis sem nome completo
  são ignorados e quem já é contato nunca é duplicado.

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

Casos sem qualquer ambiguidade — contatos com exatamente o mesmo nome e nenhum dado conflitante entre si — são fundidos automaticamente pelo **auto-merge de alta fidelidade**, que vem ligado por padrão e pode ser desligado em **Configurações → Alertas e Merge**. Todo merge automático fica registrado no histórico e pode ser desfeito.

---

## 9. Histórico e Reversão

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

### Por quanto tempo o histórico é mantido?

Os **últimos 30 snapshots** de cada contato ficam sempre visíveis na interface. No banco, os registros com mais de 30 dias são apagados na limpeza automática das madrugadas — veja [Quanto espaço o TrueContact ocupa no disco?](#quanto-espaço-o-truecontact-ocupa-no-disco).

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

*Última atualização: Agosto 2026*  
*[Reportar um problema](https://github.com/osnipassos/truecontact-releases/issues) · [Início](https://osnipassos.github.io/truecontact-releases/)*
