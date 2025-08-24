# Event Management Microservices Challenge – Descrição Detalhada Cenário do Negócio

Desenvolva um sistema de gerenciamento de eventos para uma empresa que organiza conferências, workshops e meetups. A empresa quer automatizar:

 1. Criação e gerenciamento de eventos (nome, local, data, capacidade
    máxima).
 2. Inscrição de participantes, garantindo que não excedam o limite do
    evento.
 3. Notificação de participantes sobre confirmações, alterações ou
    cancelamentos.
 4. Geração de relatórios de eventos e participantes, permitindo busca
    rápida e análises.

O sistema precisa ser modular, escalável e baseado em microsserviços, permitindo que novos módulos sejam adicionados no futuro sem impactar os existentes.

### Objetivos do Challenge
1. Criar microsserviços que simulem um sistema real de eventos, incluindo:
- Registro de eventos
- Inscrição de participantes
- Notificações assíncronas
- Relatórios e consultas rápidas
2. Aplicar padrões modernos de mercado, como:
- DDD e Clean Architecture
- Microsserviços independentes
- Event-driven architecture via Kafka ou RabbitMQ
3. Implementar persistência e cache eficientes, mensageria, segurança e observabilidade.
4. Criar testes unitários e de integração para validar o comportamento crítico do sistema.

### Fluxo de Dados Entre Microsserviços
#### Event Service
- Recebe requisições REST para criar, atualizar ou consultar eventos.
- Publica eventos de criação/atualização em Kafka/RabbitMQ (event.created, event.updated).
- Persiste informações no PostgreSQL.

#### Registration Service
- Recebe inscrições de participantes via REST.
- Valida se o evento ainda possui vagas disponíveis.
- Publica evento participant.registered.
- Atualiza cache em Redis para consulta rápida de vagas disponíveis.

#### Notification Service
- Consome eventos do Event Service e Registration Service.
- Envia notificações simuladas (console ou log) para participantes.
- Permite batch processing e envio assíncrono.

#### Report Service (opcional)
- Consome eventos para gerar relatórios analíticos.
- Armazena dados em Elasticsearch para consultas rápidas.
- Gera relatórios diários, mensais ou por evento.

### Requisitos Técnicos Detalhados

#### Linguagem & Frameworks
- Java 17+
- Spring Boot 3.x
- Spring Data JPA / Hibernate
- MapStruct para DTO ↔ Entity

#### Arquitetura & Padrões
- Microsserviços independentes (mínimo 3)
- DDD e Clean/Hexagonal Architecture
- REST APIs com OpenAPI/Swagger
- Comunicação assíncrona via Kafka ou RabbitMQ

#### Banco de Dados
- PostgreSQL para dados principais
- Redis para cache de consultas rápidas
- Elasticsearch para relatórios e buscas avançadas
- Flyway ou Liquibase para versionamento de schema

#### Segurança
- JWT/OAuth2 para autenticação
- Spring Security para proteção de endpoints
- Keycloak opcional como Identity Provider

#### DevOps e Observabilidade
- Docker + Docker Compose para todos os serviços
- Métricas via Prometheus + Grafana
- Tracing distribuído via Zipkin ou OpenTelemetry
- Logs centralizados via ELK Stack (opcional)

#### Testes
- Unitários: JUnit 5 + Mockito
- Integração: Testcontainers (PostgreSQL, Kafka, Redis)
- Cobertura mínima sugerida: 70%

### Critérios de Avaliação Detalhados

1. **Funcionalidade**
    - Serviços implementados corretamente, fluxo de inscrição e notificações funcionando.
2. **Arquitetura e Design** 
    - Separação de responsabilidades, modularidade e escalabilidade.
    - Uso correto de DDD e Clean Architecture.
3. **Qualidade do Código**
    - Legibilidade, organização e boas práticas.
    - Testes unitários e integração presentes.
4. **DevOps & Observabilidade**
    - Serviços dockerizados e fáceis de iniciar.
    - Métricas e logs implementados.
    - Tracing distribuído funcional.
5. **Segurança**
    - Endpoints críticos protegidos.
    - Autenticação funcionando corretamente.
6. **Extras / Diferenciais**
    - Interface web simples para visualização de eventos/inscrições.
    - Suporte a múltiplos tipos de notificação.
    - Implementação de sagas ou fallback para falhas de inscrição.
    - Kubernetes manifests para deploy (opcional).

### Entregáveis
- Repositório Git com:
	- Microsserviços dockerizados
	- Scripts de criação de banco de dados
	- Documentação completa (README.md)
	- Testes unitários e de integração
   
---
by GPT
