# Gerador de Calendário Java (Backend)

Um sistema backend em Java que gera calendários personalizados através de uma API REST. O sistema permite a criação de calendários para diferentes meses, anos e formatos, incluindo suporte a feriados brasileiros e eventos personalizados.

## Características

- **API REST** completa para geração de calendários
- **Suporte a múltiplos formatos** (JSON, texto, CSV)
- **Feriados brasileiros** incluídos automaticamente
- **Eventos personalizados** configuráveis
- **Múltiplos locales** (pt-BR, en-US, es-ES)
- **Configuração flexível** do primeiro dia da semana
- **Documentação automática** com Swagger/OpenAPI
- **Validação de dados** robusta

## Tecnologias Utilizadas

- Java 17
- Spring Boot 3.2.0
- Maven
- Jackson (JSON)
- Swagger/OpenAPI
- JUnit (testes)

## Estrutura do Projeto

```
src/main/java/com/calendar/generator/
├── controller/          # Controllers REST
├── service/            # Lógica de negócio
├── dto/                # Data Transfer Objects
├── config/             # Configurações
└── CalendarGeneratorApplication.java
```

## Instalação e Execução

### Pré-requisitos

- Java 17 ou superior
- Maven 3.6 ou superior

### Executando a aplicação

1. Clone o repositório
2. Navegue até o diretório do projeto
3. Execute os comandos:

```bash
# Compilar o projeto
mvn clean compile

# Executar a aplicação
mvn spring-boot:run
```

A aplicação estará disponível em: `http://localhost:8080`

### Documentação da API

Acesse a documentação interativa da API em:
- Swagger UI: `http://localhost:8080/swagger-ui.html`
- OpenAPI JSON: `http://localhost:8080/api-docs`

## Endpoints da API

### 1. Calendário Mensal

```http
GET /api/calendar/{year}/{month}
```

**Parâmetros:**
- `year` (obrigatório): Ano (1900-2100)
- `month` (obrigatório): Mês (1-12)
- `locale` (opcional): Locale (pt-BR, en-US, etc.) - padrão: pt-BR
- `firstDayOfWeek` (opcional): Primeiro dia da semana (SUNDAY, MONDAY) - padrão: SUNDAY
- `includeHolidays` (opcional): Incluir feriados - padrão: true
- `includeWeekNumbers` (opcional): Incluir números das semanas - padrão: false
- `format` (opcional): Formato de saída (json, text, csv) - padrão: json

**Exemplo:**
```http
GET /api/calendar/2024/12?locale=pt-BR&firstDayOfWeek=MONDAY&format=json
```

### 2. Calendário Anual

```http
GET /api/calendar/{year}
```

**Parâmetros:**
- `year` (obrigatório): Ano (1900-2100)
- `locale` (opcional): Locale - padrão: pt-BR

**Exemplo:**
```http
GET /api/calendar/2024?locale=pt-BR
```

### 3. Calendário Personalizado

```http
POST /api/calendar/custom
```

**Body (JSON):**
```json
{
  "year": 2024,
  "month": 12,
  "locale": "pt-BR",
  "firstDayOfWeek": "MONDAY",
  "includeHolidays": true,
  "includeWeekNumbers": false,
  "format": "json",
  "customEvents": [
    {
      "date": "2024-12-25",
      "title": "Natal",
      "description": "Celebração do Natal",
      "type": "HOLIDAY",
      "color": "#ff0000"
    }
  ]
}
```

### 4. Calendário do Mês Atual

```http
GET /api/calendar/current
```

**Parâmetros:**
- `locale` (opcional): Locale - padrão: pt-BR

### 5. Verificação de Saúde

```http
GET /api/calendar/health
```

## Formatos de Resposta

### JSON (Padrão)
Retorna um objeto JSON estruturado com todas as informações do calendário.

### Texto
Retorna o calendário formatado como texto simples.

### CSV
Retorna os dados do calendário em formato CSV para exportação.

## Feriados Suportados

### Feriados Nacionais Brasileiros

- Confraternização Universal (1º de Janeiro)
- Carnaval (Segunda e Terça-feira)
- Sexta-feira Santa
- Tiradentes (21 de Abril)
- Dia do Trabalhador (1º de Maio)
- Independência do Brasil (7 de Setembro)
- Nossa Senhora Aparecida (12 de Outubro)
- Finados (2 de Novembro)
- Proclamação da República (15 de Novembro)
- Natal (25 de Dezembro)

### Feriados Móveis

- Carnaval (calculado baseado na Páscoa)
- Sexta-feira Santa
- Páscoa
- Corpus Christi

## Exemplos de Uso

### Gerar calendário de dezembro de 2024

```bash
curl "http://localhost:8080/api/calendar/2024/12?locale=pt-BR&format=json"
```

### Gerar calendário anual de 2024

```bash
curl "http://localhost:8080/api/calendar/2024?locale=pt-BR"
```

### Gerar calendário personalizado

```bash
curl -X POST "http://localhost:8080/api/calendar/custom" \
  -H "Content-Type: application/json" \
  -d '{
    "year": 2024,
    "month": 12,
    "locale": "pt-BR",
    "firstDayOfWeek": "MONDAY",
    "includeHolidays": true,
    "customEvents": [
      {
        "date": "2024-12-31",
        "title": "Réveillon",
        "type": "CUSTOM"
      }
    ]
  }'
```

## Configuração

As configurações da aplicação podem ser alteradas no arquivo `src/main/resources/application.yml`:

```yaml
calendar:
  default-locale: pt-BR
  supported-locales: pt-BR,en-US,es-ES
  max-year: 2100
  min-year: 1900
```

## Testes

Para executar os testes:

```bash
mvn test
```

## Contribuição

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Suporte

Para suporte ou dúvidas, abra uma issue no repositório do projeto.

