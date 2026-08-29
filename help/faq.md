# TrueContact — Manual do Usuário

> **Versão do documento:** Agosto 2026  
> Encontrou um erro ou tem uma pergunta não respondida? [Abra uma issue](https://github.com/osnipassos/truecontact-releases/issues).

---

## Índice

1. [Primeiros Passos](#1-primeiros-passos)
2. [Segurança e Privacidade](#2-segurança-e-privacidade)
3. [Sincronização de Contatos](#3-sincronização-de-contatos)
4. [Conectar o Google Contacts](#4-conectar-o-google-contacts)
5. [Conectar o LinkedIn e o Facebook](#5-conectar-o-linkedin-e-o-facebook)
6. [Conectar o WhatsApp](#6-conectar-o-whatsapp)
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

## 5. Conectar o LinkedIn e o Facebook

As duas redes são **fontes de enriquecimento**: o TrueContact lê perfis públicos para preencher os seus contatos, mas nunca publica, comenta ou envia nada em seu nome.

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

## 6. Conectar o WhatsApp

### Passo a passo: leitura do QR Code

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
| Ícone WhatsApp | Verde | Números aguardando verificação no WhatsApp |
| Ícone Google | Azul Google | Contatos aguardando sincronização com o Google Contacts |
| Ícone Apple | Cinza | Contatos aguardando sincronização com o iCloud |

Quando há itens em fila, o ícone da respectiva rede anima com um efeito pulsante. Os badges desaparecem quando a fila é processada.

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
