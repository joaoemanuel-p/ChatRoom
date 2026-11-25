# 💬 ChatRoom

Aplicativo mobile de mensagens em tempo real desenvolvido com React Native, Expo e Supabase. Permite criar salas públicas, conversar com outros usuários, acompanhar quem está online e visualizar indicadores de digitação, com atualização automática das mensagens.

Projeto acadêmico desenvolvido no curso de Análise e Desenvolvimento de Sistemas (ADS) do IESB.

## 🎯 Objetivo

Desenvolver uma aplicação mobile de comunicação que permita aos usuários criar e participar de salas públicas, trocar mensagens em tempo real e interagir com outros participantes.

O projeto utiliza autenticação, banco de dados PostgreSQL e recursos de comunicação em tempo real, com foco em organização da aplicação, experiência do usuário e segurança das informações.

## 🚀 Funcionalidades

- Cadastro de usuários com e-mail e senha;
- Login e gerenciamento de sessão;
- Criação automática de perfil após o cadastro;
- Nome de exibição e avatar com cor personalizada;
- Listagem de salas públicas;
- Visualização da quantidade de participantes;
- Criação de salas com emoji e descrição;
- Entrada e saída de salas;
- Envio e recebimento de mensagens em tempo real;
- Atualização automática das conversas com Supabase Realtime;
- Envio otimista de mensagens, com exibição imediata;
- Indicador de usuários online;
- Indicador de digitação em tempo real;
- Exclusão das próprias mensagens;
- Edição do nome exibido no perfil;
- Controle de acesso às conversas utilizando Row Level Security (RLS).

## 🛠️ Tecnologias

| Tecnologia | Utilização |
|---|---|
| React Native | Desenvolvimento da aplicação mobile |
| Expo SDK 58 | Ambiente de desenvolvimento |
| Expo Router | Navegação e organização das telas |
| TypeScript | Tipagem e organização do código |
| Supabase | Backend e autenticação |
| PostgreSQL | Banco de dados relacional |
| Supabase Auth | Cadastro, login e gerenciamento de sessão |
| Supabase Realtime | Comunicação e atualização em tempo real |
| Row Level Security (RLS) | Controle de acesso aos dados |
| TanStack Query | Gerenciamento e cache de dados |
| Zod | Validação de dados |
| @hookform/resolvers | Integração de validação de formulários |
| Jest | Testes automatizados |
| PGlite | Testes do banco de dados |
| Prettier | Padronização do código |

## 📁 Estrutura do projeto

```text
ChatRoom/
├── app/                    # Rotas e telas da aplicação
├── assets/                 # Imagens e recursos visuais
├── src/
│   ├── components/         # Componentes reutilizáveis
│   ├── context/            # Contexto de autenticação
│   ├── hooks/              # Hooks personalizados
│   ├── services/           # Serviços e integração com Supabase
│   └── utils/              # Funções auxiliares
├── supabase/
│   ├── schema.sql          # Estrutura do banco e políticas
│   └── tests/              # Testes do banco de dados
├── __tests__/              # Testes automatizados da aplicação
├── assets/
├── .env.example            # Exemplo das variáveis de ambiente
├── .gitignore
├── app.json
├── App.tsx
├── index.ts
├── package.json
├── package-lock.json
├── tsconfig.json
└── README.md
```

## ⚙️ Configuração e execução

### Pré-requisitos

- Node.js;
- npm;
- Expo Go ou ambiente compatível;
- Conta no Supabase.

### 1. Instalação

Clone o repositório:

```bash
git clone https://github.com/joaoemanuel-p/ChatRoom.git
cd ChatRoom
```

Instale as dependências:

```bash
npm ci
```

### 2. Configuração do Supabase

Crie um projeto no [Supabase](https://supabase.com) e execute o arquivo:

```text
supabase/schema.sql
```

Esse arquivo configura a estrutura do banco de dados, as políticas de segurança, os relacionamentos e os recursos necessários para o funcionamento das salas e mensagens.

O banco utiliza tabelas específicas para usuários, salas, mensagens e participação nas salas.

Após executar o schema, acesse **Database → Replication** e confirme que a tabela `messages` está habilitada para Realtime.

### 3. Variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto utilizando `.env.example` como referência:

```env
EXPO_PUBLIC_SUPABASE_URL=https://SEU-PROJETO.supabase.co
EXPO_PUBLIC_SUPABASE_KEY=SUA-CHAVE-ANON-OU-PUBLISHABLE
```

Substitua os valores pelos dados públicos de conexão do seu projeto Supabase.

Não compartilhe credenciais privadas nem envie arquivos `.env` para o GitHub.

### 4. Inicialização

Depois de instalar as dependências e configurar o ambiente, inicie o aplicativo:

```bash
npx expo start
```

Abra o projeto utilizando o Expo Go ou outro ambiente compatível com React Native.

## 🔒 Segurança e controle de acesso

A segurança é implementada utilizando os recursos do PostgreSQL e do Supabase.

Entre os principais mecanismos estão:

- Autenticação de usuários pelo Supabase Auth;
- Políticas de Row Level Security (RLS);
- Controle de participação por meio da tabela `room_members`;
- Restrição de acesso às mensagens conforme a participação do usuário na sala;
- Função `is_room_member` para auxiliar na validação das permissões;
- Gatilho no PostgreSQL para criação automática do perfil após o cadastro.

A tabela `room_members` é importante para garantir que o acesso às mensagens dependa da participação efetiva na sala, e não apenas da navegação entre telas.

## ⚡ Comunicação em tempo real

O ChatRoom utiliza os recursos do Supabase Realtime para manter as conversas atualizadas entre os participantes.

São utilizados três mecanismos:

- **Postgres Changes:** acompanha alterações nas mensagens armazenadas no banco;
- **Presence:** identifica e contabiliza os usuários conectados à sala;
- **Broadcast:** transmite eventos temporários, como os indicadores de digitação.

O envio otimista permite que as mensagens apareçam imediatamente na interface, enquanto a confirmação da operação acontece em seguida.

O indicador de digitação é temporário e não precisa ser armazenado como uma mensagem no banco de dados.

## 🧪 Testes

O projeto possui testes automatizados para a aplicação e para as operações relacionadas ao banco de dados.

| Comando | Função |
|---|---|
| `npm test` | Executa os testes da aplicação e do banco |
| `npm run test:app` | Testa agrupamento de mensagens, avatar e indicador de digitação |
| `npm run test:db` | Testa RLS, gatilho de perfil e políticas de participação nas salas |
| `npm run typecheck` | Verifica a tipagem TypeScript |
| `npm run format` | Formata os arquivos do projeto |

Os testes do banco utilizam PGlite, permitindo executar operações PostgreSQL localmente sem necessidade de Docker.

A execução das suítes no ambiente local é necessária para confirmar os resultados dos testes.

## 🏗️ Arquitetura

A aplicação está organizada em camadas para separar responsabilidades:

- **app:** navegação, rotas e telas;
- **components:** elementos visuais reutilizáveis;
- **context:** gerenciamento da sessão do usuário;
- **hooks:** lógica de salas, mensagens, presença e digitação;
- **services:** comunicação com o Supabase;
- **utils:** funções auxiliares para mensagens, avatares e indicadores;
- **supabase:** estrutura do banco, regras de segurança e testes.

## 📌 Status do projeto

Aplicação estruturada com autenticação, salas públicas, mensagens em tempo real, presença de participantes, indicadores de digitação e controle de acesso utilizando Supabase.

## 👨‍💻 Autor

**João Emanuel Pinheiro Leite**

Análise e Desenvolvimento de Sistemas — IESB.

## 🔗 Repositório

[https://github.com/joaoemanuel-p/ChatRoom](https://github.com/joaoemanuel-p/ChatRoom)
