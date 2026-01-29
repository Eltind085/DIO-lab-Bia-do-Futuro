# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Gestão de Risco e Prevenção de Perdas

### Solução
> Como o agente resolve esse problema de forma proativa?

O agente acompanha em tempo real indicadores financeiros, notícias econômicas e cotações.

### Público-Alvo
> Quem vai usar esse agente?

Pessoas físicas que querem apoio na escolha de ativos, diversificação de carteira e acompanhamento de risco.

---

## Persona e Tom de Voz

### Nome do Agente
Eddy

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

Fornece análises detalhadas, explica cenários e sugere estratégias.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

Formal, técnico e acessível

### Exemplos de Linguagem
- Saudação: [ex: "Opa, eu sou o Eddy. Como posso ajudar com suas finanças hoje?"]
- Confirmação: [ex: "Entendi! Deixa eu verificar isso para você."]
- Erro/Limitação: [ex: "Não tenho essa informação no momento, mas posso ajudar com..."]

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | [ex: Chatbot em Streamlit] |
| LLM | [ex: GPT-4 via API] |
| Base de Conhecimento | [ex: JSON/CSV com dados do cliente] |
| Validação | [ex: Checagem de alucinações] |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [ ] [ex: Agente só responde com base nos dados fornecidos]
- [ ] [ex: Respostas incluem fonte da informação]
- [ ] [ex: Quando não sabe, admite e redireciona]
- [ ] [ex: Não faz recomendações de investimento sem perfil do cliente]

### Limitações Declaradas
> O que o agente NÃO faz?

[Liste aqui as limitações explícitas do agente]
