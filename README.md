# Desafio Itaú Unibanco - Backend

![Build Status](https://img.shields.io/github/workflow/status/leandrordg/springboot-desafio-itau/CI?label=Build&logo=github)
![License](https://img.shields.io/github/license/leandrordg/springboot-desafio-itau)
![Java Version](https://img.shields.io/badge/Java-17-blue)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.4-brightgreen)

Este repositório contém a solução para o desafio de programação proposto pelo Itaú Unibanco. O desafio consiste em criar uma API REST que recebe transações e retorna estatísticas baseadas nessas transações.

A aplicação foi desenvolvida utilizando **Java** com **Spring Boot**, e os dados são armazenados em memória utilizando a estrutura **ConcurrentLinkedQueue**.

## Requisitos do Projeto

### Endpoints da API

A API implementa os seguintes endpoints:

1. **POST `/transacao`**  
   Recebe transações e as armazena em memória. Cada transação contém um valor e uma data/hora de ocorrência.

2. **DELETE `/transacao`**  
   Limpa todos os dados de transações armazenados.

3. **GET `/estatistica`**  
   Retorna as estatísticas das transações que ocorreram nos últimos 60 segundos. As estatísticas incluem:
   - Quantidade de transações
   - Soma total dos valores das transações
   - Média dos valores
   - Menor valor
   - Maior valor

### Requisitos Técnicos

- **Tecnologia**: A aplicação foi desenvolvida utilizando **Java** com **Spring Boot**.
- **Armazenamento**: Os dados são armazenados **em memória** utilizando uma **ConcurrentLinkedQueue**, que garante a segurança em acesso concorrente.
- **Formato de dados**: A API utiliza **JSON** para comunicação.

## Como Rodar o Projeto

### Pré-requisitos

- **Java 17** ou superior
- **Maven** para build (ou use o wrapper do Maven `mvnw`)

### Passos para Execução

1. Clone o repositório:
   ```bash
   git clone https://github.com/leandrordg/desafio-itau-backend.git
   ```

2. Navegue até o diretório do projeto:
   ```bash
   cd desafio-itau-backend
   ```

3. Execute o aplicativo:
   ```bash
   ./mvnw spring-boot:run
   ```

   A aplicação estará disponível em `http://localhost:8080`.

## Exemplos de Uso

### 1. Receber uma Transação: `POST /transacao`

Envie uma transação no formato JSON:

```json
{
    "valor": 300.49,
    "dataHora": "2025-03-30T20:15:10.789-03:00"
}
```

Resposta:
- **201 Created**: Quando a transação for válida e armazenada.
- **422 Unprocessable Entity**: Quando a transação for inválida.
- **400 Bad Request**: Quando o formato JSON estiver errado.

### 2. Limpar Transações: `DELETE /transacao`

Este endpoint limpa todas as transações armazenadas. Resposta:

- **200 OK**: Quando as transações forem apagadas com sucesso.

### 3. Calcular Estatísticas: `GET /estatistica`

Este endpoint retorna as estatísticas das transações realizadas nos últimos 60 segundos. Exemplo de resposta:

```json
{
    "count": 3,
    "sum": 500.48,
    "avg": 166.82666666666668,
    "min": 49.99,
    "max": 300.49
}
```

## Considerações de Implementação

### Validação das Transações

As transações são validadas com os seguintes critérios:

- O campo `valor` não pode ser negativo.
- O campo `dataHora` não pode ser no futuro.
- O valor da transação deve ser maior ou igual a 0.

### Armazenamento em Memória

As transações são armazenadas em memória utilizando uma **`ConcurrentLinkedQueue`**. Essa estrutura permite um acesso seguro em ambientes multithreaded, o que é importante caso haja concorrência no armazenamento das transações.

### Estatísticas

As estatísticas são calculadas apenas para transações realizadas nos últimos 60 segundos. Se não houver transações no período, as estatísticas retornam valores zero.

## Dependências Utilizadas

Este projeto utiliza as seguintes dependências do **Spring Boot**:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Essas dependências garantem o funcionamento da API, validação dos dados, e ferramentas de desenvolvimento e teste para o projeto.

## Contribuindo

Sinta-se à vontade para abrir issues ou enviar pull requests com melhorias, correções ou novas funcionalidades.

## Licença

Este projeto está licenciado sob a MIT License - veja o arquivo [LICENSE](LICENSE) para mais detalhes.
