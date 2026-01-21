# The Architecture of Gateways (TAG) v0.0.1

**Uma arquitetura de software centrada em domínio, funcional e pragmática**

[![Python](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![TypeScript](https://img.shields.io/badge/typescript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[English](./docs/en/README.md) | **Português**

> _Inspirada em Hexagonal Architecture, Diplomata (Nubank) e DOMA (Uber)_

---

## 📋 Índice

- [Motivação](#-motivação)
- [O que é TAG?](#-o-que-é-tag)
- [Linguagens Suportadas](#-linguagens-suportadas)
- [Filosofia e Princípios](#-filosofia-e-princípios)
- [Estrutura da Arquitetura](#-estrutura-da-arquitetura)
- [Camadas e Responsabilidades](#-camadas-e-responsabilidades)
- [Regras de Dependência](#-regras-de-dependência)
- [Implementação Python](#-implementação-python)
- [Implementação TypeScript](#-implementação-typescript)
- [Testes](#-testes)
- [Recomendações de Stack](#-recomendações-de-stack)
- [Exemplos Práticos](#-exemplos-práticos)
- [Comparação com Outras Arquiteturas](#-comparação-com-outras-arquiteturas)
- [FAQ](#-faq)
- [Contribuindo](#-contribuindo)
- [Roadmap](#-roadmap)

---

## 🎯 Motivação

### A Jornada: Da Startup ao Staff Engineer

O desejo de criar uma arquitetura funcional que padronize o desenvolvimento de
aplicações nasceu há mais de **5 anos**, quando fundei minha primeira startup: a
**PayParty**. Embora a empresa não tenha prosperado por questões de timing e
modelo de negócio, foi nela que comecei a adotar padrões de projeto rigorosos
para:

- **Facilitar a adoção de novas features**: Novos desenvolvedores conseguiam
  contribuir rapidamente
- **Manutenção de código sustentável**: Bugs eram fáceis de rastrear e corrigir
- **Facilidade de entendimento**: Qualquer engenheiro sabia onde encontrar o que
  precisava

Naquela época, usando **JavaScript puro e Express.js** no backend, construí
serviços padronizados mesmo sem saber que estava aplicando conceitos de
arquitetura que mais tarde se tornariam fundamentais para mim. Era uma busca
intuitiva por **consistência e previsibilidade**.

### A Validação: Nubank

Esse sentimento ficou ainda mais forte quando ingressei no **Nubank**. Lá,
observei que todos os serviços seguiam um padrão consistente para tudo:
bibliotecas, frameworks, tecnologias e arquitetura. A empresa adotava o
**Diplomata**, uma arquitetura de software bem estabelecida para serviços em
Clojure.

Foi no Nubank que meus pensamentos se consolidaram. Percebi que eu **estava
pensando certo** e **estava no caminho certo**. A arquitetura padronizada trazia
benefícios tangíveis:

- **Onboarding rápido**: Desenvolvedores se adaptavam facilmente entre times
- **Código previsível**: Todos sabiam onde encontrar o que precisavam
- **Qualidade consistente**: Padrões arquiteturais evitavam anti-patterns
- **Evolução coordenada**: Mudanças de stack eram aplicadas de forma uniforme

Essa experiência me deu **validação e razão**: padrões arquiteturais não são
apenas teoria acadêmica, mas ferramentas práticas que transformam a forma como
times desenvolvem software.

### O Gatilho: Stone

Ao ingressar na **Stone** como Staff Engineer, encontrei o cenário oposto: **não
havia padrão arquitetural para nada**. Cada time, cada projeto, seguia uma
abordagem diferente. O caos arquitetural gerava:

- ❌ Dificuldade de colaboração entre times
- ❌ Curva de aprendizado alta ao mudar de contexto
- ❌ Código inconsistente e difícil de manter
- ❌ Retrabalho de soluções já implementadas

Foi na Stone que tudo se conectou. A experiência da PayParty me ensinou a
**valorizar padrões**. O Nubank me mostrou que **padrões funcionam em escala**.
A Stone me deu o **contexto e a urgência** para criar algo novo.

### O Nascimento de TAG

Como Staff Engineer, decidi trazer um pouco da **experiência do Nubank** para
resolver esse problema na Stone, mas com **melhorias e adaptações pessoais**:

1. **Inspiração no Diplomata (Nubank)**: Organização clara, padrões bem
   definidos
2. **Adaptação para múltiplas linguagens**: Python e TypeScript como primeiras
   implementações
3. **Zero Logic in Handlers**: Simplificação radical dos pontos de entrada
4. **Railway-Oriented Programming**: Composição de pipelines com Result types
5. **Protocol-Based DI**: Testabilidade sem dependência de infraestrutura
6. **Aprendizados da PayParty**: Pragmatismo e foco em developer experience

Assim nasceu **TAG (The Architecture of Gateways)**: uma arquitetura pragmática,
funcional e centrada em domínio, forjada por anos de experiência desde a
fundação de uma startup até a atuação como Staff Engineer em fintechs de escala
global.

TAG não é apenas uma arquitetura - é a **cristalização de uma jornada** de
aprendizado sobre como criar software que escala, tanto tecnicamente quanto
organizacionalmente.

---

## 🎯 O que é TAG?

**TAG (The Architecture of Gateways)** é um padrão arquitetural que fornece uma
visão tática e estratégica para desenvolver soluções de software centradas em
domínio, com foco em:

- **Programação Funcional**: Imutabilidade, funções puras e composição via
  pipelines
- **Domain-Driven Design**: Orientação ao domínio e isolamento de regras de
  negócio
- **Railway-Oriented Programming**: Composição de Results para tratamento de
  erros
- **Zero Logic in Handlers**: Handlers são apenas pontos de entrada/saída
- **Testabilidade**: Testes unitários e de integração desacoplados de
  infraestrutura
- **Multi-linguagem**: Implementações consistentes em Python e TypeScript

---

## 🌍 Linguagens Suportadas

TAG está disponível atualmente em:

### Python 3.11+

- ✅ Implementação completa
- ✅ Exemplos práticos
- ✅ Stack recomendada: FastAPI, Pydantic, returns

### TypeScript 5.0+

- ✅ Implementação completa
- ✅ Exemplos práticos
- ✅ Stack recomendada: Express/Fastify, Zod, neverthrow

---

## 💭 Filosofia e Princípios

### Princípios Fundamentais

1. **Flows são Pipelines**: Cada Flow é uma composição funcional de
   transformações
2. **Handlers sem Lógica**: Handlers apenas conectam transporte ↔ Flows
3. **Drivers fazem Conversões**: Drivers traduzem entre mundo externo e
   aplicação
4. **Logics são Puras**: Nunca fazem IO, apenas validam e retornam primitivos
5. **Adapters Transformam Estruturas**: Convertem dados entre camadas
6. **Gateways fazem IO**: Retornam dados brutos sem transformação
7. **Protocols Definem Contratos**: Abstrações permitem trocar implementações
8. **IO nas Bordas**: Efeitos colaterais isolados nos Gateways

### Inspirações

| Arquitetura            | O que trouxemos                          |
| ---------------------- | ---------------------------------------- |
| **Hexagonal**          | Ports & Adapters, isolamento de domínio  |
| **Diplomata (Nubank)** | Organização corporativa de microservices |
| **DOMA (Uber)**        | Domain-Oriented Microservices            |
| **Railway-Oriented**   | Composição de Results via pipe/bind/map  |

---

## 📁 Estrutura da Arquitetura

A estrutura de pastas é **idêntica** em todas as linguagens, garantindo
consistência:

```
project-root/
├── src/
│   ├── protocols/          # Contratos de infraestrutura
│   ├── drivers/            # Implementações de libs externas
│   ├── gateways/           # Acesso ao mundo externo (IO)
│   ├── adapters/           # Transformações de estrutura
│   ├── logics/             # Validações e cálculos puros
│   ├── flows/              # Pipelines de casos de uso
│   ├── handlers/           # Pontos de entrada (zero lógica)
│   ├── domains/            # Entidades e schemas
│   ├── resources/          # Configs tipadas
│   └── main.[py|ts]        # Dependency injection
├── tests/
│   ├── unit/               # Testes de Adapters e Logics
│   └── integration/        # Testes de Flows completos
└── README.md
```

---

## 🏗️ Camadas e Responsabilidades

### Resumo das Camadas

| Camada        | Responsabilidade                | Características                         |
| ------------- | ------------------------------- | --------------------------------------- |
| **Protocols** | Contratos de infraestrutura     | Apenas assinaturas, sem implementação   |
| **Drivers**   | Implementações de libs externas | Convertem formatos externos ↔ aplicação |
| **Gateways**  | Acesso externo (IO)             | Funções puras que recebem Protocols     |
| **Adapters**  | Transformações de dados         | Funções puras sem efeitos colaterais    |
| **Logics**    | Validações e cálculos           | Funções puras, retornam primitivos      |
| **Flows**     | Orquestração (pipelines)        | Compõem Gateways, Logics, Adapters      |
| **Handlers**  | Pontos de entrada/saída         | Zero lógica, apenas conectam            |
| **Domains**   | Schemas e entidades             | Apenas definições, nunca funções        |
| **Resources** | Configurações                   | Schemas tipados                         |

Para detalhes completos de cada camada, consulte:

- [Guia Python](./docs/pt-br/python-guide.md)
- [Guia TypeScript](./docs/pt-br/typescript-guide.md)

---

## 🔗 Regras de Dependência

### Diagrama de Dependências

```
main.[py|ts]
   ↓
Drivers ←→ Protocols
   ↓         ↓
Handlers → Resources
   ↓
Flows
   ↓
Gateways + Logics + Adapters
   ↓
Domains
```

### Matriz de Dependências

| Camada        | Pode Chamar                                      | Não Pode Chamar                                |
| ------------- | ------------------------------------------------ | ---------------------------------------------- |
| **main**      | Drivers, Resources, Handlers                     | Flows, Gateways, Logics                        |
| **Drivers**   | Protocols, Resources                             | Handlers, Flows, Gateways                      |
| **Handlers**  | Adapters, Flows, Protocols, Resources            | Gateways, Logics, Drivers                      |
| **Flows**     | Gateways, Logics, Adapters, Protocols, Resources | Handlers, Drivers                              |
| **Gateways**  | Protocols, Domains, Adapters                     | Flows, Handlers, Logics                        |
| **Logics**    | Domains, Resources                               | Flows, Gateways, Handlers, Protocols, Adapters |
| **Adapters**  | Domains                                          | Qualquer camada com IO                         |
| **Domains**   | Nada                                             | Todas                                          |
| **Protocols** | Nada                                             | Todas                                          |
| **Resources** | Nada                                             | Todas                                          |

---

## 🐍 Implementação Python

### Stack Recomendada

```toml
[tool.poetry.dependencies]
python = "^3.11"
pydantic = "^2.5.0"
returns = "^0.22.0"
fastapi = "^0.109.0"
```

### Exemplo: Create User Flow

#### Protocol

```python
# src/protocols/database_protocol.py
from typing import Protocol, Any, Dict, List
from returns.result import Result

class DatabaseProtocol(Protocol):
    def execute_query(
        self, query: str, params: Dict[str, Any]
    ) -> Result[List[Dict[str, Any]], str]:
        ...
```

#### Domain

```python
# src/domains/user.py
from pydantic import BaseModel, EmailStr
from uuid import UUID

class UserDomain(BaseModel):
    id: UUID
    email: EmailStr
    name: str

    class Config:
        frozen = True
```

#### Logic

```python
# src/logics/user_logic.py
from returns.result import Result, Success, Failure

def validate_email_format(email: str) -> Result[str, str]:
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    if re.match(pattern, email):
        return Success(email)
    return Failure("Invalid email format")
```

#### Flow

```python
# src/flows/user/create_user_flow.py
from returns.pipeline import pipe
from returns.pointfree import bind

def create_user_flow(
    database: DatabaseProtocol,
    input_data: CreateUserInput
) -> Result[UserDomain, str]:
    return pipe(
        validate_email_format(input_data.email),
        bind(lambda email: find_user_by_email_gateway(database, email)),
        bind(has_user_in_rows),
        bind(check_user_not_exists),
        map_(lambda _: input_to_user_domain(input_data)),
        bind(lambda user: persist_user_gateway(database, user))
    )
```

**[Ver guia completo Python →](./docs/pt-br/python-guide.md)**

---

## 📘 Implementação TypeScript

<details>
<summary><strong>Clique para ver exemplos TypeScript</strong></summary>

### Stack Recomendada

```json
{
  "dependencies": {
    "express": "^4.18.0",
    "zod": "^3.22.0",
    "neverthrow": "^6.1.0"
  }
}
```

### Exemplo: Create User Flow

#### Protocol

```typescript
// src/protocols/database.protocol.ts
import { Result } from "neverthrow";

export interface DatabaseProtocol {
  executeQuery<T>(
    query: string,
    params: Record<string, any>,
  ): Promise<Result<T[], string>>;
}
```

#### Domain

```typescript
// src/domains/user.domain.ts
import { z } from "zod";

export const UserDomainSchema = z.object({
  id: z.string().uuid(),
  email: z.string().email(),
  name: z.string().min(2).max(100),
}).readonly();

export type UserDomain = z.infer<typeof UserDomainSchema>;
```

#### Logic

```typescript
// src/logics/user.logic.ts
import { err, ok, Result } from "neverthrow";

export function validateEmailFormat(email: string): Result<string, string> {
  const pattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  if (pattern.test(email)) {
    return ok(email);
  }
  return err("Invalid email format");
}
```

#### Flow

```typescript
// src/flows/user/create-user.flow.ts
export async function createUserFlow(
  database: DatabaseProtocol,
  inputData: CreateUserInput,
): Promise<Result<UserDomain, string>> {
  const emailResult = validateEmailFormat(inputData.email);
  if (emailResult.isErr()) return emailResult;

  const findResult = await findUserByEmailGateway(database, emailResult.value);
  if (findResult.isErr()) return findResult;

  // ... resto do pipeline

  return persistUserGateway(database, user);
}
```

**[Ver guia completo TypeScript →](./docs/pt-br/typescript-guide.md)**

</details>

---

## 🧪 Testes

### Python

```python
def test_validate_email_format_success():
    result = validate_email_format("user@example.com")
    assert result.is_ok()
```

<details>
<summary><strong>Ver exemplo TypeScript</strong></summary>
```typescript
it('should accept valid email', () => {
  const result = validateEmailFormat('user@example.com');
  expect(result.isOk()).toBe(true);
});
```

</details>

---

## 📚 Recomendações de Stack

| Componente      | Python   | TypeScript       |
| --------------- | -------- | ---------------- |
| **Schemas**     | Pydantic | Zod              |
| **Result Type** | returns  | neverthrow       |
| **HTTP Server** | FastAPI  | Express, Fastify |
| **Testing**     | pytest   | vitest           |

---

## 📦 Exemplos Práticos

Explore exemplos completos e funcionais:

- **[Python User Service](./examples/python/user-service/)** - CRUD completo com
  FastAPI
- **[TypeScript User Service](./examples/typescript/user-service/)** - CRUD
  completo com Express

---

## 🔍 Comparação com Outras Arquiteturas

| Aspecto             | TAG                   | Hexagonal      | Clean Arch  | DOMA       |
| ------------------- | --------------------- | -------------- | ----------- | ---------- |
| **Paradigma**       | Functional-First      | OOP/Functional | OOP         | OOP        |
| **Organização**     | Por Flow/Feature      | Por Layer      | Por Layer   | Por Domain |
| **Handlers**        | Zero Logic            | Controllers    | Controllers | Handlers   |
| **Multi-linguagem** | ✅ Python, TypeScript | ⚠️ Parcial     | ⚠️ Parcial  | ❌ Não     |

---

## ❓ FAQ

<details>
<summary><strong>Qual linguagem devo escolher?</strong></summary>

**Python** se você tem ecossistema de data science/ML ou prefere sintaxe
concisa.

**TypeScript** se você já tem infraestrutura Node.js ou precisa de performance
em I/O.

</details>

<details>
<summary><strong>As implementações são compatíveis?</strong></summary>

Sim! A estrutura e princípios são idênticos. Você pode misturar serviços em
diferentes linguagens.

</details>

<details>
<summary><strong>TAG funciona com NestJS?</strong></summary>

Sim! TAG é compatível com NestJS. O framework pode ser usado no Driver layer.

</details>

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Veja nosso
[Guia de Contribuição](CONTRIBUTING.md).

### Como Contribuir

1. Fork o repositório
2. Crie uma branch (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Add: nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

---

## 🗺️ Roadmap

### v0.1.0 (Q1 2025)

- [x] Implementação Python completa
- [x] Implementação TypeScript completa
- [ ] Exemplo: Payment Service
- [ ] CLI para scaffolding
- [ ] Documentação em inglês

### v0.2.0 (Q2 2025)

- [ ] Event Sourcing patterns
- [ ] CQRS patterns
- [ ] Observabilidade e métricas

### v1.0.0 (Q4 2025)

- [ ] Certificação TAG
- [ ] Adoção em produção
- [ ] Comunidade ativa

---

## 📄 Licença

MIT License - veja [LICENSE](LICENSE) para detalhes.

---

## 🙏 Agradecimentos

Inspirado por:

- **Alistair Cockburn** - Hexagonal Architecture
- **Nubank Engineering** - Diplomata Architecture
- **Uber Engineering** - DOMA
- **Robert C. Martin** - Clean Architecture
- **Eric Evans** - Domain-Driven Design
- **Scott Wlaschin** - Railway-Oriented Programming

Agradecimento especial às experiências na **PayParty**, **Nubank** e **Stone**.

---

<div align="center">

**Construído com ❤️ para desenvolvedores que valorizam domínio, funcionalidade e
simplicidade**

**TAG Architecture v0.0.1**

[⭐ Star](https://github.com/seu-usuario/tag-architecture) •
[📖 Docs](./docs/pt-br/) •
[💬 Discussões](https://github.com/seu-usuario/tag-architecture/discussions) •
[🐛 Issues](https://github.com/seu-usuario/tag-architecture/issues)

</div>
