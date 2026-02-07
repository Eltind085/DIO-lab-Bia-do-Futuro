# Base de Conhecimento

## Dados Utilizados

Os dados de `data`, foram usados como exemplos e modificados com `Microsoft Copilot`

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ter continuidade dos atendimentos mais efeciente |
| `perfil_investidor.json` | JSON | Personalizar as explicações sobre duvidas e necessidades do cliente |
| `produtos_financeiros.json` | JSON | Conhecer os produtos e realizar resumir ao cliente |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente e ultilizar de forma didática |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

O produto "Fundo Multimercado" foi substituido pelo atual "Fundo Imoibiliário" devido ao meu grau de conhecimento para respotas ainda mais assertivas.

---

## Estratégia de Integração

### Como os dados são carregados?
> Com duas possibilidades, podendo os dados serem injetados (CTRL + C, CTRL + V) ou carregados via código, como no exemplo abaixo.

```#python
import pandas as pd

historico = pd.read_csv(`data/historico_atendimento.csv`)
transacoes = pd.read_csv(`data/transacoes.csv`)
```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Para simplifiicar, podemos apenas "INJETAR" os dados em nosso prompt, garantindo o melhor contexto possível, reforçando que essas informações sejam carregadas de forma dinamica para termos ainda maior flexibilidade.

```text
DADOS DO CLIENTE E PERFIL (perfil_investidor.json):
{
  "nome": "Allyson Rodrigues"
  "idade": 36
  "profissao": "Empresário"
  "renda_mensal": 10.000,00
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}


TRANSAÇÕES DO CLIENTE (data/transacoes.csv):
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida
2025-10-28,Shopping,lazer,320.00,saida
2025-10-30,Empréstimo Bradesco,financeiro,1500.00,entrada
2025-11-01,Salário,receita,5000.00,entrada
2025-11-02,Aluguel,moradia,1200.00,saida
2025-11-03,Supermercado,alimentacao,480.00,saida
2025-11-05,Spotify,lazer,34.90,saida
2025-11-07,Farmácia,saude,75.00,saida
2025-11-10,Restaurante,alimentacao,150.00,saida
2025-11-12,Uber,transporte,60.00,saida
2025-11-15,Conta de Água,moradia,95.00,saida
2025-11-18,Parcela Empréstimo Bradesco,financeiro,300.00,saida
2025-11-20,Academia,saude,99.00,saida
2025-11-22,Viagem,lazer,800.00,saida
2025-11-25,Combustível,transporte,270.00,saida
2025-11-28,Freelance,receita,1200.00,entrada
2025-11-30,Empréstimo Bradesco,financeiro,2000.00,entrada

PRODUTOS DÍSPONIVEIS PARA LESIONAR (data/produtos_financeiros.json):
[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "102% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Imobiliários (FII)",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "Dividend yield entre 8% a 12% ao ano",
    "aporte_minimo": 1  0.00,
    "indicado_para": "Perfil moderado que busca diversificação e renda recorrente mensal"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  }
]

HISTÓRICO DE ATENDIMENTO DO CLIENTE (data/historico_atendimento.csv)
data,canal,tema,resumo,resolvido
2025-09-15,chat,CDB,Cliente perguntou sobre rentabilidade e prazos,sim
2025-09-22,telefone,Problema no app,Erro ao visualizar extrato foi corrigido,sim
2025-10-01,chat,Tesouro Selic,Cliente pediu explicação sobre o funcionamento do Tesouro Direto,sim
2025-10-12,chat,Metas financeiras,Cliente acompanhou o progresso da reserva de emergência,sim
2025-10-25,email,Atualização cadastral,Cliente atualizou e-mail e telefone,sim
2025-11-03,telefone,Cartão de crédito,Cliente relatou cobrança indevida e foi estornada,sim
2025-11-10,chat,Investimentos em ações,Cliente pediu orientação sobre riscos da bolsa,sim
2025-11-18,email,Problema de login,Cliente não conseguia acessar conta; senha redefinida,sim
2025-11-25,chat,Planejamento de aposentadoria,Cliente solicitou simulação de previdência privada,sim
2025-12-02,telefone,Empréstimo pessoal,Cliente questionou taxas de juros e recebeu proposta revisada,sim
2025-12-10,email,Erro em boleto,Cliente recebeu boleto duplicado; corrigido,sim
2025-12-18,chat,Fundos imobiliários,Cliente pediu explicação sobre liquidez e riscos,sim
2025-12-27,telefone,Problema no app,Cliente não conseguia gerar comprovante de pagamento; corrigido,sim
2026-01-05,email,Atualização cadastral,Cliente alterou endereço residencial,sim
2026-01-12,chat,Reserva de emergência,Cliente pediu recomendação sobre valor ideal,sim
2026-01-20,telefone,Cartão bloqueado,Cliente teve cartão bloqueado por suspeita de fraude; desbloqueado após verificação,sim
2026-01-28,chat,Investimento em dólar,Cliente perguntou sobre vantagens e riscos da moeda estrangeira,sim
2026-02-03,email,Problema financeiro,Cliente relatou dificuldade em pagar parcelas do empréstimo; renegociação iniciada,sim
2026-02-07,chat,Planejamento financeiro,Cliente pediu ajuda para equilibrar gastos mensais,sim
```

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.
O exemplo descrito abaixo tem como base nos dados originais da base de conhecimentos, mas os sintetiza deixando apenas informações relevantes otimizando o uso de tokens. Entretanto, mais importante que economizar token, tenhamos de se assegurar de ter todas as informações relevantes disponíveis no contexto.

```
Dados do Cliente:
- Nome: Allyson Rodrigues
- Perfil: Moderado
- Saldo disponível: R$ 15.000

RESUMO DE GASTOS:
- Moradia: R$ 2.450
- Alimentação: R$ 800
- Transporte: R$ 500
- Saúde: R$ 250
- Lazer: R$ 1.000
- Total de saídas: 5.000

PRODUTOS DISPONÍVEIS PARA EXPLICAR:
- Tesouro Celic (risco baixo)
- CBD Liquidez Diária (risco baixo a médio)
- LCI/LCA (risco baixo a médio)
- Fundo imobiliário (FIIs) (Médio)
- Fundo de ações (Alto)
...
```
