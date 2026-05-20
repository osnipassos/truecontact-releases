# TrueContact — Manual do Usuário

> **Versão do documento:** Maio 2026  
> Encontrou um erro ou tem uma pergunta não respondida? [Abra uma issue](https://github.com/osnipassos/truecontact-releases/issues).

---

## Índice

1. [Primeiros Passos](#1-primeiros-passos)
2. [Segurança e Privacidade](#2-segurança-e-privacidade)
3. [Sincronização de Contatos](#3-sincronização-de-contatos)
4. [Conectar o Google Contacts](#4-conectar-o-google-contacts)
5. [Conectar o WhatsApp](#5-conectar-o-whatsapp)
6. [Templates e Automações](#6-templates-e-automações)
7. [Operações em Lote e Indicadores](#7-operações-em-lote-e-indicadores)
8. [Atualizações](#8-atualizações)

---

## 1. Primeiros Passos

### O que é o TrueContact?

O **TrueContact** é um CRM pessoal automático para Mac e Windows. Liga-se ao iCloud, ao Google Contacts, ao LinkedIn e ao WhatsApp para **sincronizar, enriquecer e organizar** os seus contatos — e envia mensagens de aniversário e de acompanhamento automaticamente, em segundo plano.

Ao contrário das soluções cloud (HubSpot, Salesforce, etc.), o TrueContact roda **100% no seu computador**. Não há subscrição, não há conta, não há servidor para salvar os seus dados.

### Para quem é?

- Profissionais de networking que querem manter contatos sempre atualizados
- Quem usa o iPhone/Mac e quer tirar o máximo partido do iCloud Contacts
- Quem usa o Gmail e precisa manter o Google Contacts em sincronia com o iCloud
- Quem quer enviar parabéns automáticos sem parecer um bot
- Quem valoriza a **privacidade total** dos seus dados de contato

### Requisitos do sistema

| Plataforma | Versão mínima |
|---|---|
| macOS | 13 Ventura ou superior |
| Windows | 10 (64-bit) ou superior |

### Como instalar

1. Acesse à [página de Releases](https://github.com/osnipassos/truecontact-releases/releases/latest)
2. Baixe o arquivo para o seu sistema operativo:
   - **macOS:** arquivo `.dmg`
   - **Windows:** arquivo `.exe` (instalador)
3. **macOS:** Abra o `.dmg`, arraste o TrueContact para a pasta Aplicações
4. **Windows:** Execute o instalador e siga os passos
5. Na primeira abertura, o **Assistente de Configuração** guia você por cada etapa

> **Importante (macOS):** Se o sistema mostrar o aviso "app de desenvolvedor desconhecido", vá a **Configurações do Sistema → Privacidade e Segurança** e clique em "Abrir na mesma". O TrueContact não está na App Store por opção — isso é intencional para manter o app gratuito.

### Assistente de Configuração (Onboarding Wizard)

Na primeira abertura, o TrueContact exibe um **assistente de configuração passo a passo** que guia você por todas as integrações:

1. **Boas-vindas** — visão geral do hub-and-spoke
2. **Apple iCloud** — inserção do Apple ID e App-Specific Password
3. **Google Contacts** — autenticação OAuth com a sua conta Google
4. **LinkedIn** — autenticação e configuração dos radares automáticos
5. **WhatsApp** — leitura do QR Code
6. **Agendamento** — frequência e janela horária das varreduras automáticas
7. **Normalização** — prefixos, sufixos e formatos de nome
8. **Templates** — mensagens de aniversário personalizadas
9. **Alertas e Merge** — prévia do sistema de detecção de duplicados
10. **Tudo pronto!** — links de ajuda e feedback

Você pode rever o assistente a qualquer momento em **Configurações → Refazer Setup Inicial**.

### Primeira configuração manual (alternativa ao assistente)

Se preferir configurar manualmente:

1. **Configurar o iCloud** — insira o Apple ID e a App-Specific Password para importar os seus contatos
2. **Conectar o Google Contacts** — autorize via OAuth nas Configurações
3. **Conectar o WhatsApp** — leia o QR Code nas Configurações para ativar o envio de mensagens
4. **Criar templates de aniversário** — defina as mensagens automáticas que o sistema vai enviar
5. **Deixar rodar** — o TrueContact faz tudo o resto em segundo plano

---

## 2. Segurança e Privacidade

### Os seus dados nunca saem do seu computador

Esta é a promessa central do TrueContact: **os seus dados são seus e ficam no seu computador**.

Toda a informação dos seus contatos — nomes, telefones, emails, notas, histórico de mensagens, fotos de perfil — é armazenada num banco de dados **SQLite local**, numa pasta de dados do aplicativo no seu disco rígido. Não existe nenhum servidor TrueContact a receber, processar ou armazenar esses dados.

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
| WhatsApp Web | Enviar mensagens e ler fotos de perfil | **Não** — conexão direta WhatsApp |
| GitHub Releases | Verificar se há atualizações | **Não** — só verifica um número de versão |

**Nenhuma dessas conexões passa pelos servidores TrueContact** — porque esses servidores simplesmente não existem.

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
- **LinkedIn** — cargo, empresa, foto de perfil, redes sociais
- **WhatsApp** — foto de perfil do número de telefone

O processo de sincronização funciona assim:

1. **Pull do iCloud** — Lê todos os contatos e grupos via CardDAV, preservando ETags para detectar alterações
2. **Pull do Google** — Lê alterações desde o último sync via SyncToken
3. **Enriquecimento LinkedIn** — Para contatos com perfil LinkedIn, importa cargo, empresa, foto e redes sociais
4. **Enriquecimento WhatsApp** — Para contatos com número de telefone, verifica a foto de perfil
5. **Push para iCloud e Google** — Escreve as alterações de volta em ambos os provedores

> **Regra fundamental:** O TrueContact **nunca apaga dados manuais**. Se adicionar uma nota ou um email a um contato no iPhone, essa informação é preservada mesmo que o LinkedIn devolva um campo vazio.

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

### Normalização de números de telefone

Para unir corretamente um contato do iCloud com a sua conta WhatsApp, o sistema precisa comparar números de telefone. O mesmo número pode estar guardado de formas muito diferentes:

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

## 5. Conectar o WhatsApp

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

---

## 6. Templates e Automações

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

---

## 7. Operações em Lote e Indicadores

### Excluir múltiplos contatos de uma vez

Na lista lateral (sidebar), você pode selecionar e excluir vários contatos ao mesmo tempo:

1. Clique no ícone de **seleção múltipla** no topo da sidebar
2. Marque os contatos que deseja excluir (checkbox ao lado de cada nome)
3. Clique em **"Excluir selecionados"**
4. Confirme a exclusão na caixa de diálogo

> **Atenção:** A exclusão remove o contato do banco local e enfileira a remoção nos provedores conectados (iCloud e Google). Esta ação não pode ser desfeita.

### Merge em lote

Também é possível selecionar múltiplos contatos e enviá-los diretamente para o **Merge Inteligente**:

1. Selecione 2 ou mais contatos na sidebar
2. Clique em **"Fazer Merge"**
3. O sistema abre a tela de merge com os contatos pré-selecionados

### Indicadores de fila no cabeçalho

O cabeçalho do TrueContact mostra badges coloridos indicando contatos aguardando sincronização:

| Badge | Cor | Significado |
|---|---|---|
| Ícone LinkedIn | Azul LinkedIn | Contatos na fila de enriquecimento LinkedIn |
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

---

## 8. Atualizações

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

*Última atualização: Maio 2026*  
*[Reportar um problema](https://github.com/osnipassos/truecontact-releases/issues) · [Início](https://osnipassos.github.io/truecontact-releases/)*
