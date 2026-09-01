## **Documento de Requisitos**

**Histórico de Revisão**

|Data|Versão|Descrição|Autor|
| - | - | - | - |
|27/08/2026|0.1|Versão inicial dos requisitos do Performance Lab|Equipe do projeto|
|01/09/2026|0.2|Adição da funcionalidade de organização autônoma dos dias de treino pelo aluno, com validação inteligente de combinações desconfortáveis ou lesivas|Equipe do projeto|

## **1. Introdução**

### **1.1 Propósito**
Este documento tem como objetivo especificar os requisitos funcionais e não funcionais do sistema Performance Lab, servindo como referência para o desenvolvimento, validação e evolução da solução.

### **1.2 Escopo**
O sistema permite que personal trainers organizem treinos, acompanhem o progresso dos alunos e reduzam riscos de lesões por excesso de carga ou ausência de descanso. Também oferece ao aluno uma rotina clara, com registro de exercícios, cargas e acompanhamento de evolução.

### **1.3 Definições, Acrônimos e Abreviações**

|Termo|Definição|
| - | - |
|PT|Personal Trainer|
|Aluno|Usuário que realiza o treino|
|Treino|Plano de exercícios semanal ou mensal|
|Carga|Peso, intensidade ou esforço registrado durante o exercício|

### **1.4 Referências**
- Documento de visão do projeto Performance Lab
- Material da disciplina de Construção de Software
- Estudo de caso sobre acompanhamento de alunos e gestão de academias

## **2. Descrição Geral**

### **2.1 Perspectiva do Produto**
O sistema é uma aplicação nova, voltada para gestão de treinos e acompanhamento de desempenho em academias. Ele substitui o uso de planilhas, cadernos e mensagens informais, centralizando informações em um único ambiente.

### **2.2 Funções do Produto**
O produto deve permitir:
- cadastro de alunos
- criação e organização de treinos
- organização autônoma, pelo aluno, dos dias da semana em que cada treino será realizado
- validação inteligente das combinações de treinos escolhidas pelo aluno, impedindo arranjos desconfortáveis ou lesivos
- acompanhamento de cargas, séries e repetições
- monitoramento de evolução ao longo do tempo
- alertas de risco por sobrecarga ou descanso insuficiente
- comunicação entre personal trainer e aluno

### **2.3 Características dos Usuários**
Os usuários são principalmente:
- personal trainers, que utilizam o sistema para planejar e controlar o treinamento dos alunos;
- alunos, que acompanham a rotina de treino e registram as cargas executadas.

### **2.4 Restrições**
- O sistema deve ser simples de usar para pessoas com pouco domínio tecnológico.
- Deve garantir segurança das informações pessoais e de acompanhamento físico.
- O produto deve se adequar ao contexto de academias e treinamento individualizado.

### **2.5 Suposições e Dependências**
- O personal trainer é responsável pela criação e ajuste do treino.
- O aluno pode registrar informações do treino no dia a dia.
- O aluno pode distribuir os treinos já definidos pelo personal trainer entre os dias da semana de sua preferência, respeitando as validações automáticas do sistema.
- Os usuários possuem acesso a um dispositivo com internet para uso do sistema.

## **3. Requisitos Funcionais**

Requisitos funcionais descrevem **o que o sistema deve fazer**.

| ID | Descrição | Prioridade |
| -- | --------- | :--------: |
| RF01 | O sistema deve permitir o cadastro de alunos com dados básicos e objetivos de treino. | Alta |
| RF02 | O sistema deve permitir ao personal trainer criar e editar treinos personalizados. | Alta |
| RF03 | O sistema deve permitir que o aluno visualize sua rotina semanal de treinos. | Alta |
| RF04 | O sistema deve registrar cargas, séries e repetições informadas pelo aluno. | Alta |
| RF05 | O sistema deve armazenar o histórico de progresso de cada aluno ao longo do tempo. | Alta |
| RF06 | O sistema deve apresentar indicadores de evolução de desempenho. | Média |
| RF07 | O sistema deve emitir alertas quando houver risco de sobrecarga, lesão ou ausência de recuperação adequada. | Alta |
| RF08 | O sistema deve permitir a comunicação entre personal trainer e aluno dentro da plataforma. | Média |
| RF09 | O sistema deve permitir que o personal trainer acompanhe a execução dos treinos por aluno. | Alta |
| RF10 | O sistema deve permitir ajustes na rotina do treino conforme evolução ou necessidade do aluno. | Média |
| RF11 | O sistema deve permitir que o aluno organize e distribua seus treinos nos dias da semana de sua preferência. | Alta |
| RF12 | O sistema deve impedir automaticamente combinações de treinos, em um mesmo dia ou em dias consecutivos, consideradas desconfortáveis ou com risco de lesão, sugerindo ao aluno um rearranjo adequado. | Alta |

> **Prioridade:** Alta, Média ou Baixa, conforme impacto direto no objetivo do produto e na redução dos problemas de acompanhamento e lesões.

## **4. Requisitos Não Funcionais**

Requisitos não funcionais descrevem **qualidades e restrições técnicas** do sistema.

| ID | Categoria | Descrição | Prioridade |
| -- | --------- | --------- | :--------: |
| RNF01 | Desempenho | O sistema deve responder às ações do usuário em tempo adequado para uso diário. | Alta |
| RNF02 | Segurança | O sistema deve autenticar usuários e proteger dados sensíveis. | Alta |
| RNF03 | Usabilidade | A interface deve ser intuitiva para personal trainers e alunos sem grande experiência digital. | Alta |
| RNF04 | Disponibilidade | O sistema deve estar acessível sempre que o usuário precisar consultar ou registrar treino. | Média |
| RNF05 | Manutenibilidade | O código deve ser organizado para facilitar alterações futuras e evolução do produto. | Alta |
| RNF06 | Confiabilidade | O sistema deve preservar registros de treino e evolução para manter rastreabilidade do acompanhamento. | Alta |

## **5. Regras de Negócio**

| ID | Descrição |
| -- | --------- |
| RN01 | Cada aluno deve estar vinculado a um personal trainer responsável. |
| RN02 | O personal trainer é responsável por criar e ajustar o treinamento do aluno. |
| RN03 | O aluno pode registrar apenas o desempenho do treino atribuído ao seu plano atual. |
| RN04 | O sistema deve considerar a recuperação e o descanso como fatores para alertar sobre riscos de lesão. |
| RN05 | Treinos repetidos sem variação e sem descanso adequado devem ser sinalizados como potencialmente prejudiciais. |
| RN06 | A evolução do aluno deve ser registrada e consultada no histórico do sistema. |
| RN07 | O aluno pode escolher livremente em quais dias da semana realizar cada treino atribuído pelo personal trainer, sem alterar o conteúdo (exercícios, séries, cargas) definido pelo treino. |
| RN08 | O sistema deve bloquear ou alertar a tentativa de agendar, no mesmo dia ou em dias consecutivos sem descanso mínimo, treinos que trabalhem o mesmo grupo muscular ou que sejam classificados como incompatíveis, impedindo a confirmação do arranjo até que o conflito seja resolvido. |

## **6. Protótipos**
Os protótipos podem incluir telas de:
- login
- dashboard do personal trainer
- cadastro de alunos
- criação de treino
- organização semanal dos treinos pelo aluno, com alerta de combinações inválidas
- acompanhamento do aluno
- histórico de progresso
- alertas de segurança

A implementação pode evoluir para incluir imagens, wireframes ou links de protótipos no futuro.
