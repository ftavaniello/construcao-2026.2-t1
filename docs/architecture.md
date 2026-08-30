## **Documento de Arquitetura de Software**

**Histórico de Revisão**

|Data|Versão|Descrição|Autor|
| - | - | - | - |
|30/08/2026|0.1|Versão inicial|Equipe de Desenvolvimento|

## **1. Introdução**

### **1.1 Finalidade**
Este documento apresenta uma visão geral da arquitetura de software da aplicação de gerenciamento de treinos de usuários. O objetivo é especificar as decisões arquiteturais, componentes principais e tecnologias utilizadas para garantir um desenvolvimento coerente e de fácil manutenção.

### **1.2 Escopo**
Este documento descreve a arquitetura de uma aplicação mobile de gerenciamento de treinos de musculação, incluindo o frontend mobile, backend API e banco de dados. Este documento é direcionado aos desenvolvedores, arquitetos e stakeholders do projeto, garantindo que o padrão arquitetural proposto seja seguido durante o desenvolvimento.

### **1.3 Definições, Acrônimos e Abreviações**

|Abreviação|Definição|
| - | - |
|API|Application Programming Interface|
|REST|Representational State Transfer|
|CRUD|Create, Read, Update, Delete|
|UX|User Experience|
|UI|User Interface|

### **1.4 Visão Geral**
Este documento está organizado em seções que cobrem: (2) a representação da arquitetura com o diagrama de componentes; (3) as metas e restrições arquiteturais; (4) a visão lógica com a organização do código e componentes; (5) a visão de implementação com o banco de dados; (6) considerações de desempenho e (7) atributos de qualidade.

## **2. Representação da Arquitetura**
A aplicação segue um estilo arquitetural em **camadas com separação clara entre frontend e backend**, caracterizando-se como uma arquitetura cliente-servidor com componentes especializados no backend. O frontend é uma aplicação mobile desenvolvida em React Native, enquanto o backend utiliza uma arquitetura de componentes microserviços lógicos sobre uma única API REST em FastAPI, todos comunicando-se através de endpoints RESTful e compartilhando um banco de dados PostgreSQL centralizado.

### **2.1 Diagrama de Relações**

```
                        ┌─────────────────────────┐
                        │  Aplicação Mobile       │
                        │  [React Native]         │
                        └────────────┬────────────┘
                                     │
                    ┌────────────────┼────────────────┐
                    │                │                │
            ┌───────▼────────┐  ┌────▼──────────┐  ┌─▼──────────────┐
            │ Gerenciamento  │  │ Planejamento  │  │   Execução de  │
            │  de Usuários   │  │    Semanal    │  │    Treinos     │
            │  [Component]   │  │  [Component]  │  │  [Component]   │
            └────────────────┘  └────────────────┘  └────────────────┘
                                     │
                    ┌────────────────┼────────────────┐
                    │                │                │
            ┌───────▼────────┐  ┌────▼──────────┐  ┌─▼──────────────┐
            │  Gerenciamento │  │   Progressão  │  │  Backend API   │
            │    de Treinos  │  │   e Alertas   │  │   [FastAPI]    │
            │  [Component]   │  │  [Component]  │  └────────────────┘
            └────────────────┘  └────────────────┘          │
                                                             │
                                                    ┌────────▼────────┐
                                                    │  Banco de Dados │
                                                    │  [PostgreSQL]   │
                                                    └─────────────────┘
```

## **3. Metas e Restrições de Arquitetura**

|**Restrição**|**Ferramenta**|
| :- | :- |
|Linguagem Backend|Python|
|Linguagem Frontend|JavaScript/TypeScript|
|Framework Backend|FastAPI|
|Framework Frontend|React Native|
|Plataforma|Mobile (iOS e Android)|
|Banco de Dados|PostgreSQL|
|Segurança|Autenticação JWT, HTTPS/TLS, Validação de entrada|
|Idioma|Português (Brasil)|
|Padrão de Arquitetura|Cliente-Servidor com Componentes Especializados|
|Comunicação|REST API com JSON|

## **4. Visão Lógica**

### **4.1 Visão geral: Pacotes e Camadas**

A aplicação segue uma arquitetura em **3 camadas principais**:

1. **Camada de Apresentação (Frontend Mobile)**
   - Responsabilidade: Interface com usuário e personal trainer
   - Tecnologia: React Native
   - Componentes: Telas de autenticação, dashboard, planejamento e execução de treinos

2. **Camada de Aplicação (Backend API)**
   - Responsabilidade: Lógica de negócio e orquestração
   - Tecnologia: FastAPI (Python)
   - Componentes especializados:
     - **Gerenciamento de Usuários**: Autenticação, autorização e perfis
     - **Planejamento Semanal**: Criação e organização de treinos semanais
     - **Execução de Treinos**: Registro e acompanhamento em tempo real
     - **Gerenciamento de Treinos**: CRUD de exercícios e séries
     - **Progressão e Alertas**: Análise de dados e notificações

3. **Camada de Persistência (Banco de Dados)**
   - Responsabilidade: Armazenamento e recuperação de dados
   - Tecnologia: PostgreSQL
   - Entidades: Usuários, Treinos, Exercícios, Registros de Execução, Progressões

### **4.2 Organização do Código**

```
projeto/
├── frontend/                          # Aplicação Mobile
│   ├── src/
│   │   ├── screens/                  # Componentes de tela
│   │   ├── components/               # Componentes reutilizáveis
│   │   ├── services/                 # Serviços de API
│   │   ├── stores/                   # Gerenciamento de estado
│   │   └── utils/                    # Utilitários
│   └── package.json
│
├── backend/                          # API Backend
│   ├── app/
│   │   ├── main.py                   # Entry point
│   │   ├── core/                     # Configurações e constantes
│   │   ├── api/
│   │   │   └── routes/               # Endpoints REST
│   │   │       ├── usuarios.py
│   │   │       ├── planejamento.py
│   │   │       ├── execucao.py
│   │   │       ├── treinos.py
│   │   │       └── progressao.py
│   │   ├── models/                   # Modelos de dados
│   │   ├── schemas/                  # Schemas de validação
│   │   ├── services/                 # Lógica de negócio
│   │   └── database/                 # Configuração de BD
│   ├── requirements.txt
│   └── Dockerfile
│
└── docs/                             # Documentação
    ├── architecture.md
    └── requirements.md
```

### **4.3 Diagrama de Classes**

**Classe: Usuario**
```
- id: UUID
- nome: String
- email: String (único)
- senha: String (hash)
- tipo_usuario: Enum(Cliente, PersonalTrainer)
- data_criacao: DateTime
+ autenticar(): boolean
+ atualizar_perfil(): void
```

**Classe: Treino**
```
- id: UUID
- usuario_id: UUID (FK)
- data: DateTime
- descricao: String
- duracao_minutos: Integer
+ adicionar_exercicio(): void
+ remover_exercicio(): void
```

**Classe: Exercicio**
```
- id: UUID
- treino_id: UUID (FK)
- nome: String
- series: Integer
- repeticoes: Integer
- peso_kg: Decimal
+ atualizar(): void
```

**Classe: Progressao**
```
- id: UUID
- usuario_id: UUID (FK)
- data_registro: DateTime
- peso_atual: Decimal
- observacoes: String
+ calcular_progresso(): float
```

## **5. Visão de Implementação**

### **5.1 Diagrama de Entidade-Relacionamento**

```
Usuarios (1) ────────── (N) Treinos
    │                          │
    │                          │
    │                      (1) │ (N)
    │                      Exercicios
    │
    │
    └────────────────────────── (N) Progressoes

Tabela: Usuarios
- id (PK)
- nome
- email (UNIQUE)
- senha
- tipo_usuario
- data_criacao
- data_atualizacao

Tabela: Treinos
- id (PK)
- usuario_id (FK)
- data
- descricao
- duracao_minutos
- data_criacao

Tabela: Exercicios
- id (PK)
- treino_id (FK)
- nome
- series
- repeticoes
- peso_kg
- data_criacao

Tabela: Progressoes
- id (PK)
- usuario_id (FK)
- data_registro
- peso_atual
- observacoes
```

### **5.2 Diagrama Lógico de Dados**

```
USUARIOS
├── id (UUID) - Chave Primária
├── nome (VARCHAR(255)) - NOT NULL
├── email (VARCHAR(255)) - NOT NULL, UNIQUE
├── senha (VARCHAR(255)) - NOT NULL (hash bcrypt)
├── tipo_usuario (ENUM) - 'cliente' ou 'personal_trainer'
├── ativo (BOOLEAN) - NOT NULL, default: true
└── timestamps (created_at, updated_at)

TREINOS
├── id (UUID) - Chave Primária
├── usuario_id (UUID) - Chave Estrangeira → USUARIOS.id
├── data (TIMESTAMP) - NOT NULL
├── descricao (TEXT)
├── duracao_minutos (INTEGER)
├── status (ENUM) - 'planejado', 'em_andamento', 'concluido'
└── timestamps (created_at, updated_at)

EXERCICIOS
├── id (UUID) - Chave Primária
├── treino_id (UUID) - Chave Estrangeira → TREINOS.id
├── nome (VARCHAR(255)) - NOT NULL
├── series (INTEGER) - NOT NULL
├── repeticoes (INTEGER) - NOT NULL
├── peso_kg (DECIMAL(10,2))
├── tempo_descanso_seg (INTEGER)
└── timestamps (created_at, updated_at)

PROGRESSOES
├── id (UUID) - Chave Primária
├── usuario_id (UUID) - Chave Estrangeira → USUARIOS.id
├── data_registro (TIMESTAMP) - NOT NULL
├── peso_atual (DECIMAL(10,2))
├── percentual_gordura (DECIMAL(5,2))
├── observacoes (TEXT)
└── timestamps (created_at, updated_at)
```

## **6. Tamanho e Desempenho**

### **Projeção de Volume de Dados**
- **Usuários**: Inicialmente 100-500, escalonável para 5.000+
- **Treinos**: ~2-3 por usuário por semana = ~2.600 treinos/mês (em 500 usuários)
- **Exercícios**: ~30-50 por usuário = média 10.000/mês
- **Registros de Progressão**: ~1 por usuário por semana = ~2.000/mês

### **Considerações de Desempenho**
- **Concorrência**: API deve suportar 100+ requisições simultâneas
- **Latência**: Tempo de resposta máximo de 2 segundos para operações CRUD
- **Sincronização**: Suportar sincronização offline no mobile com cache local
- **Armazenamento**: Banco de dados com índices nas colunas de busca frequente (usuario_id, data)
- **Escalabilidade Horizontal**: Backend preparado para deployment em containers (Docker) e orquestração (Kubernetes)
- **Cache**: Implementação de cache Redis para dados frequentemente acessados

## **7. Qualidade**

A arquitetura escolhida favorece os seguintes atributos de qualidade:

### **Escalabilidade**
- Separação clara entre frontend e backend permite escalar independentemente
- API RESTful permite adicionar novos componentes sem afetar existentes
- Banco de dados centralizado com índices apropriados
- Suporte para replicação e distribuição de dados

### **Manutenibilidade**
- Componentes especializados no backend (cada um com responsabilidade única)
- Código organizado em camadas claramente definidas
- Uso de frameworks estabelecidos (FastAPI, React Native)
- Documentação de arquitetura centralizada

### **Testabilidade**
- Separação clara de responsabilidades facilita testes unitários
- API com endpoints bem definidos para testes de integração
- Possibilidade de testes end-to-end com aplicação mobile

### **Segurança**
- Autenticação via JWT tokens
- Comunicação segura com HTTPS/TLS
- Validação de entrada em todos os endpoints
- Hash de senhas com bcrypt
- Isolamento de dados por usuário

### **Confiabilidade**
- Tratamento de erros estruturado
- Logging centralizado
- Backup automático do banco de dados
- Recuperação de falhas graceful

### **Usabilidade**
- Interface mobile nativa e responsiva
- Suporte offline com sincronização posterior
- Feedback visual de operações em andamento

## **8. Referências**

1. **FastAPI Documentation**: https://fastapi.tiangolo.com/
2. **React Native Documentation**: https://reactnative.dev/
3. **PostgreSQL Documentation**: https://www.postgresql.org/docs/
4. **REST API Best Practices**: Richardson Maturity Model
5. **Software Architecture Patterns**: Building Microservices - Sam Newman
6. **API Security**: OWASP API Security Top 10
7. **Docker & Containerization**: Docker Official Documentation
8. **Database Design**: Database Design for Mere Mortals - Michael J. Hernandez
