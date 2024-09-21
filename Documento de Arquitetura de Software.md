
---

# Documento de Arquitetura de Software

## 1. Visão Geral do Sistema
O **ForgeMyHero** é um sistema que estou desenvolvendo para facilitar a criação automática de fichas de personagens para **Dungeons & Dragons (D&D)**. O objetivo é simplificar o processo de criação para jogadores de todos os níveis, oferecendo um fluxo guiado que auxilia novos jogadores a entender as regras do jogo e, ao mesmo tempo, proporcionando agilidade para os jogadores mais experientes.

### 1.1 Objetivos do Documento
Neste documento, explico a arquitetura geral do sistema ForgeMyHero, incluindo as principais decisões de design, os componentes do sistema e como eles interagem. Isso deve proporcionar uma visão clara sobre a estrutura e as tecnologias envolvidas, facilitando o desenvolvimento colaborativo no futuro.

### 1.2 Tecnologias Utilizadas
- **Front-end**: React.js
- **Back-end**: Spring Boot (Java)
- **Banco de Dados**: PostgreSQL
- **Autenticação e Autorização**: OAuth 2.0 / JWT
- **Infraestrutura**: AWS (ou outro serviço em nuvem, a ser definido)
- **Sistema de Controle de Versão**: GitHub

---

## 2. Arquitetura Geral
Eu segui o padrão **MVC (Model-View-Controller)** para separar responsabilidades e garantir que o sistema seja escalável e fácil de manter. O sistema é uma aplicação web dividida em front-end e back-end, que se comunicam via APIs REST.

### 2.1 Diagrama de Arquitetura (Simplificado)

```plaintext
+------------------+       +----------------------+       +-----------------+
|     Front-end    |       |      Back-end        |       |  Banco de Dados |
|  (React.js)      |<----->|   (Spring Boot API)  |<----->|   (PostgreSQL)   |
+------------------+       +----------------------+       +-----------------+
        |                          |
        |      +-------------------+
        +----->|   Autenticação    |
               |   (OAuth 2.0 / JWT)|
               +-------------------+
```

### 2.2 Camadas do Sistema
1. **Camada de Apresentação (Front-end)**: Desenvolvida em React.js, essa camada interage diretamente com o usuário, fornecendo a interface gráfica para criação de fichas. Ela se comunica com o back-end via APIs REST, enviando e recebendo dados para preencher automaticamente as informações do personagem.

2. **Camada de Aplicação (Back-end)**: Desenvolvida em Spring Boot (Java), essa camada lida com a lógica de negócio e as regras de D&D. Ela expõe as APIs necessárias para que o front-end possa criar, modificar e consultar fichas de personagens. Também lida com a autenticação e autorização dos usuários, além de validar regras customizadas (Homebrew).

3. **Camada de Persistência (Banco de Dados)**: Utilizo o PostgreSQL para armazenar informações sobre fichas de personagens, raças, classes, e regras customizadas. A comunicação com o back-end é feita via JPA/Hibernate.

4. **Autenticação e Autorização**: O sistema utiliza **OAuth 2.0** e **JWT (JSON Web Tokens)** para autenticar e autorizar os usuários, garantindo a segurança dos dados.

---

## 3. Componentes Principais

### 3.1 Front-end (React.js)
- **Componentes de Interface**: Exibem o formulário de criação de ficha e atualizam a ficha em tempo real com base nas escolhas do jogador.
- **Comunicação com API**: Realiza chamadas REST para o back-end para buscar e enviar dados.
- **Gerenciamento de Estado**: O estado da aplicação será gerenciado utilizando Redux ou Context API para manter a consistência entre as páginas.

### 3.2 Back-end (Spring Boot)
- **Controladores (Controllers)**: Expõem APIs REST para receber as requisições do front-end e delegam a lógica de negócio para os serviços.
- **Serviços (Services)**: Contêm a lógica de criação automática de fichas, aplicação das regras de D&D e validação de regras customizadas.
- **Repositórios (Repositories)**: Gerenciam a persistência de dados, interagindo com o banco de dados via JPA/Hibernate.

### 3.3 Banco de Dados (PostgreSQL)
- **Tabelas Principais**:
  - **Users**: Armazena as informações de usuários autenticados.
  - **Characters**: Armazena as fichas de personagens.
  - **Races, Classes, Backgrounds**: Armazena as opções de criação de personagens.
  - **CustomRules**: Armazena regras customizadas (Homebrew) criadas pelos usuários.

---

## 4. Padrões de Projeto Utilizados

- **Factory Pattern**: Para a criação de personagens com base nas escolhas de raça, classe e background.
- **Repository Pattern**: Para gerenciar o acesso ao banco de dados de forma desacoplada.
- **Builder Pattern**: Para montar a ficha do personagem de forma incremental, conforme as opções são escolhidas.

---

## 5. Requisitos Não Funcionais

- **Escalabilidade**: O sistema será escalável, com capacidade de atender múltiplos usuários simultâneos e suportar crescimento futuro.
- **Segurança**: Implementarei HTTPS, OAuth 2.0 e JWT para proteger os dados e garantir a privacidade dos usuários.
- **Desempenho**: O sistema será otimizado para baixa latência, com tempo de resposta rápido durante o preenchimento e atualização das fichas.
- **Disponibilidade**: O sistema terá alta disponibilidade, com um tempo de uptime de 99,9%, e suporte a backups e recuperação de dados.

---

## 6. Decisões Arquiteturais

### 6.1 Padrão MVC
Escolhi o padrão de arquitetura **MVC** (Model-View-Controller) para separar a lógica de negócio, apresentação e controle, o que facilita a manutenção e o crescimento do projeto.

### 6.2 Spring Boot e React.js
A escolha por **Spring Boot** e **React.js** se deve à sua flexibilidade, popularidade e capacidade de integração com outras tecnologias, como PostgreSQL e OAuth.

### 6.3 PostgreSQL
Escolhi o **PostgreSQL** por ser um banco de dados robusto e open-source, amplamente utilizado no mercado, e com bom suporte para dados relacionais complexos.

---
