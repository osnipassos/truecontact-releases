# TrueContact — Manual do Usuário

> **Versão do documento:** Maio 2026  
> Encontraste um erro ou tens uma pergunta não respondida? [Abre uma issue](https://github.com/osnipassos/truecontact-releases/issues).

---

## Índice

1. [Primeiros Passos](#1-primeiros-passos)
2. [Segurança e Privacidade](#2-segurança-e-privacidade)
3. [Sincronização de Contatos](#3-sincronização-de-contatos)
4. [Conectar o WhatsApp](#4-conectar-o-whatsapp)
5. [Templates e Automações](#5-templates-e-automações)
6. [Atualizações](#6-atualizações)

---

## 1. Primeiros Passos

### O que é o TrueContact?

O **TrueContact** é um CRM pessoal automático para Mac e Windows. Liga-se ao iCloud, ao LinkedIn e ao WhatsApp para **sincronizar, enriquecer e organizar** os teus contatos — e envia mensagens de aniversário e de acompanhamento automaticamente, em segundo plano.

Ao contrário das soluções cloud (HubSpot, Salesforce, etc.), o TrueContact corre **100% no teu computador**. Não há subscrição, não há conta, não há servidor a salvar os seus dados.

### Para quem é?

- Profissionais de networking que querem manter contatos sempre atualizados
- Quem usa o iPhone/Mac e quer tirar o máximo partido do iCloud Contacts
- Quem quer enviar parabéns automáticos sem parecer um bot
- Quem valoriza a **privacidade total** dos seus dados de contato

### Requisitos do sistema

| Plataforma | Versão mínima |
|---|---|
| macOS | 13 Ventura ou superior |
| Windows | 10 (64-bit) ou superior |

### Como instalar

1. Acede à [página de Releases](https://github.com/osnipassos/truecontact-releases/releases/latest)
2. Baixe o ficheiro para o teu sistema operativo:
   - **macOS:** ficheiro `.dmg`
   - **Windows:** ficheiro `.exe` (instalador)
3. **macOS:** Abre o `.dmg`, arrasta o TrueContact para a pasta Aplicações
4. **Windows:** Executa o instalador e segue os passos
5. Na primeira abertura, vai a **Configurações** e introduz as credenciais do iCloud

> **Importante (macOS):** Se o sistema mostrar o aviso "app de desenvolvedor desconhecido", vai a **Configurações do Sistema → Privacidade e Segurança** e clica em "Abrir na mesma". O TrueContact não está na App Store por opção — isso é intencional para manter a app gratuita.

### Primeira configuração

Após instalar, o fluxo recomendado é:

1. **Configurar o iCloud** — introduz o Apple ID e a App-Specific Password para importar os teus contatos
2. **Conectar o WhatsApp** — lê o QR Code nas Configurações para ativar o envio de mensagens
3. **Criar templates de aniversário** — define as mensagens automáticas que o sistema vai enviar
4. **Deixar correr** — o TrueContact faz tudo o resto em segundo plano

---

## 2. Segurança e Privacidade

### Os seus dados nunca saem do seu computador

Esta é a promessa central do TrueContact: **os teus dados são teus e ficam no teu computador**.

Toda a informação dos teus contatos — nomes, telefones, emails, notas, histórico de mensagens, fotos de perfil — é armazenada numa base de dados **SQLite local**, numa pasta de dados da aplicação no teu disco rígido. Não existe nenhum servidor TrueContact a receber, processar ou armazenar esses dados.

A base de dados encontra-se em:

- **macOS:** `~/Library/Application Support/truecontact/database.sqlite`
- **Windows:** `%APPDATA%\truecontact\database.sqlite`

Podes abrir, copiar ou fazer backup deste ficheiro em qualquer momento com ferramentas como o [DB Browser for SQLite](https://sqlitebrowser.org/).

### O que é enviado para a internet?

O TrueContact apenas faz conexões com a internet para:

| Conexão | Finalidade | Os teus dados passam pelos servidores TrueContact? |
|---|---|---|
| iCloud CardDAV | Sincronizar contatos com o iCloud | **Não** — conexão direta Apple |
| LinkedIn | Ler perfis públicos dos teus contatos | **Não** — só leitura, sem envio |
| WhatsApp Web | Enviar mensagens e ler fotos de perfil | **Não** — conexão direta WhatsApp |
| GitHub Releases | Verificar se há atualizações | **Não** — só verifica um número de versão |

**Nenhuma dessas conexões passa pelos servidores TrueContact** — porque esses servidores simplesmente não existem.

### Sessão do WhatsApp

Quando ligas o WhatsApp ao TrueContact através do QR Code, é gerado um **ficheiro de sessão local** que mantém a tua autenticação. Este ficheiro fica em:

- **macOS:** `~/Library/Application Support/truecontact/whatsapp-session/`
- **Windows:** `%APPDATA%\truecontact\whatsapp-session\`

> **Aviso:** Nunca compartilhes esta pasta com ninguém. Quem tiver acesso a estes ficheiros pode enviar mensagens em teu nome. Se suspeitas de comprometimento, vai a **WhatsApp → Configurações → Dispositivos conectados** e remove a sessão TrueContact.

### App-Specific Password do iCloud

O TrueContact usa uma **App-Specific Password** para aceder ao iCloud Contacts — nunca a tua password principal do Apple ID. Se a password for comprometida, podes revogá-la sem alterar o teu Apple ID ou afetar o restante da conta.

Para gerar uma, vai a [appleid.apple.com](https://appleid.apple.com) → **Iniciar sessão e segurança → Senhas específicas de app**.

---

## 3. Sincronização de Contatos

### Como o TrueContact une dados de várias fontes

O TrueContact funciona como um **Hub central**: o iCloud é a fonte de verdade principal, e o LinkedIn e o WhatsApp enriquecem esses contatos com dados adicionais.

O processo de sincronização funciona assim:

1. **Pull do iCloud** — Lê todos os contatos e grupos via CardDAV, preservando ETags para detetar alterações
2. **Enriquecimento LinkedIn** — Para contatos com perfil LinkedIn, visita automaticamente o perfil e importa cargo, empresa, foto e redes sociais
3. **Enriquecimento WhatsApp** — Para contatos com número de telefone, verifica a foto de perfil (se autorizado pelo contato)
4. **Push para o iCloud** — Escreve as alterações de volta no iCloud, ficando disponíveis no iPhone, iPad e Mac

> **Regra fundamental:** O TrueContact **nunca apaga dados manuais**. Se adicionares uma nota ou um email a um contato no iPhone, essa informação é preservada mesmo que o LinkedIn devolva um campo vazio.

### Normalização de números de telefone

Para unir corretamente um contato do iCloud com a sua conta WhatsApp, o sistema precisa de comparar números de telefone. O mesmo número pode estar guardado de formas muito diferentes:

| Formato no iCloud | Formato no WhatsApp |
|---|---|
| `(11) 98765-4321` | `5511987654321` |
| `+55 11 9 8765-4321` | `5511987654321` |
| `11 8765-4321` (sem 9º dígito) | `5511987654321` |

O TrueContact normaliza automaticamente todos estes formatos, incluindo a adição do **9º dígito** para números brasileiros mais antigos. Assim, um número guardado como `11 8765-4321` é corretamente identificado como o mesmo que `5511987654321` no WhatsApp.

### Porque não vejo a foto de alguns contatos do WhatsApp?

Esta é uma das perguntas mais comuns. A resposta é simples: **o WhatsApp respeita as configurações de privacidade de cada utilizador**.

Se um contato configurou a sua foto de perfil para ser visível apenas para os seus próprios contatos (ou para ninguém), o WhatsApp não disponibiliza essa foto a nenhuma aplicação — incluindo o TrueContact. Quando isso acontece, o TrueContact mostra um **ícone de privacidade** em vez da foto, sinalizando que o contato existe no WhatsApp mas optou por restringir a visibilidade da sua imagem.

**Isto é um comportamento correto, não um bug.** O TrueContact respeita as escolhas de privacidade dos teus contatos da mesma forma que o próprio WhatsApp faz.

> **Dica:** Se quiseres ver a foto real de um contato específico, pede-lhe que abra as configurações de privacidade do WhatsApp → Foto de perfil → "Todos os Meus Contatos".

---

## 4. Conectar o WhatsApp

### Passo a passo: leitura do QR Code

**No TrueContact:**

1. Abre as **Configurações** (ícone de engrenagem no canto superior direito)
2. Vai à secção **WhatsApp**
3. Clica em **"Conectar WhatsApp"**
4. Um **QR Code** aparecerá no tela — tens 60 segundos para o ler

**No teu celular (iOS ou Android):**

1. Abre o **WhatsApp**
2. Vai a **Definições → Dispositivos conectados**
3. Toca em **"Conectar um dispositivo"**
4. Aponta a câmara para o QR Code no tela do computador
5. Aguarda a confirmação

> **Nota:** O TrueContact aparece como "Chrome em [nome do computador]" na lista de aparelhos ligados. O WhatsApp permite até 4 dispositivos ao mesmo tempo.

### Resolver problemas de conexão

**O QR Code expira antes de conseguir ler:**
Clica em "Atualizar QR Code" nas Configurações. O código é regenerado instantaneamente.

**"Sessão desligada" aparece nas Configurações:**
O WhatsApp desliga dispositivos inativos por mais de 14 dias. Repete o processo de conexão.

**O WhatsApp diz "Número de aparelhos atingido":**
Remove um dispositivo existente em **WhatsApp → Configurações → Dispositivos conectados** e tenta novamente.

---

## 5. Templates e Automações

### O que são templates?

Os **templates** são mensagens pré-configuradas que o TrueContact envia automaticamente em determinados eventos — principalmente aniversários. Podes criar múltiplos templates para o mesmo evento, e o sistema sorteia qual usar, tornando as mensagens mais naturais e variadas.

### Criar uma mensagem de aniversário

1. Abre as **Configurações**
2. Vai à secção **Templates de Aniversário**
3. Clica em **"Adicionar Template"**
4. Escreve a mensagem, usando a variável `{{nome_amigavel}}` para personalizar
5. Clica em **"Salvar"**

**Exemplo:**
```
Olá {{nome_amigavel}}! 🎂 Hoje é o teu dia especial — muitas felicidades e que este novo ano traga tudo o que mereces! 🥳
```

### A variável `{{nome_amigavel}}`

A variável `{{nome_amigavel}}` é substituída pelo nome mais natural do contato, seguindo esta ordem de prioridade:

1. **Apelido (Nickname)** — se definido no iCloud (ex: `Zé`)
2. **Primeiro nome** — se não tiver apelido (ex: `José`)
3. **Nome completo** — apenas como último recurso

**Porquê esta lógica?**  
Imagine que tens guardado o teu amigo como "José Manuel Ferreira da Silva" no iCloud, mas toda a gente o chama de "Zé". Se o apelido "Zé" estiver definido, a mensagem será *"Olá Zé! 🎂..."* em vez de *"Olá José Manuel Ferreira da Silva! 🎂..."* — muito mais natural.

> **Dica:** Para adicionar um apelido no iPhone, abre o contato → "Editar" → "adicionar campo" → "Apelido".

### Sorteio de mensagens e delay de digitação

**1. Sorteio aleatório:**  
Quando há múltiplos templates, o sistema escolhe um aleatoriamente. O mesmo contato receberá uma mensagem diferente a cada aniversário.

**2. Delay de digitação (simulação humana):**  
Antes de enviar, o TrueContact ativa o indicador "a escrever..." no WhatsApp e aguarda um tempo proporcional ao comprimento da mensagem — como se estivesses a escrever manualmente. Isto reduz significativamente a probabilidade de as mensagens serem marcadas como spam.

> **Aviso:** Não configures templates com linguagem de marketing ou links promocionais. Os templates devem ser mensagens genuínas e pessoais.

---

## 6. Atualizações

### Como funciona a atualização automática

O TrueContact usa um sistema de **atualização OTA (Over-The-Air)** — silencioso, automático e seguro.

**O processo:**

1. Quando a app inicia, verifica discretamente se existe uma versão mais recente
2. Se encontrar uma versão nova, **baixa em segundo plano** sem interromper o teu trabalho
3. Quando a download estiver completo, uma **notificação discreta** pergunta se queres instalar agora ou na próxima abertura
4. A atualização é instalada e a app reinicia automaticamente

**Segurança:**  
Cada ficheiro de atualização é **assinado criptograficamente** antes de ser publicado. O TrueContact verifica esta assinatura antes de instalar — se a assinatura não corresponder, a atualização é rejeitada automaticamente.

> **Nota:** As atualizações são publicadas no repositório público `osnipassos/truecontact-releases`. O código-fonte nunca é publicado nesse repositório — apenas os binários compilados e assinados.

### Ver a versão atual

Consulta a versão instalada em **Configurações → Sobre o TrueContact**, no fundo da página.

---

*Última atualização: Maio 2026*  
*[Reportar um problema](https://github.com/osnipassos/truecontact-releases/issues) · [Início](https://osnipassos.github.io/truecontact-releases/)*
