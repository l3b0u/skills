---
name: imagen-gpt
description: Use when /imagen-gpt should force OpenAI image route.
version: 0.1.0
author: Henri Claude Le Bourlegat, Claude Arcanjuz
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [image-generation, openai, chatgpt, cost-guard]
    related_skills: [imagen]
---

# /imagen-gpt Skill

## When to Use

Use esta skill quando Henri pedir `/imagen-gpt <pedido>` ou disser explicitamente que quer gerar imagem pela rota ChatGPT/OpenAI.

## Regra principal

Esta é uma rota direta: **não compare fornecedores por padrão**. Use ChatGPT/OpenAI Images, salvo se houver bloqueio de credencial, custo anormal, endpoint indisponível ou risco técnico relevante.

## Procedimento

1. Carregue também a skill `imagen` e siga as regras gerais de segurança, arquivos, referências reais, log lateral e verificação.
2. Na skill `imagen`, carregue a ficha de ChatGPT/OpenAI antes de executar.
3. Antes de executar, informe custo estimado da rota escolhida quando houver custo por API/créditos. Se for uso via assinatura/login ChatGPT/Codex, registrar como `incluído na assinatura` ou `custo marginal não apurado`, sem inventar valor.
4. Se o pedido envolve texto legível, UI, peça de campanha, embalagem ou copy na imagem, mantenha esta rota como preferencial.
5. Salve mídia + JSON lateral com `fornecedor: "chatgpt|openai"` e o modelo real usado.

## Nota Open Design — skill não é connector

Esta skill aparece em Open Design como **skill/recipe**, não como `connector` de projeto. Portanto, `connectors: []` não significa que a skill esteja ausente. Connectors são integrações externas como Composio/Canva/GitHub; `/imagen-gpt` é uma rota operacional/skill.

Se a geração raster pela OpenAI não estiver disponível dentro do agente Open Design, use o fallback correto: gerar pelo Hermes `/imagen-gpt` fora do Open Design, salvar o arquivo localmente, copiar para `assets/imagen/` do projeto Open Design e registrar JSON lateral. Não invente que `@imagen-gpt` é um conector.

## Quando parar

- Falta de `OPENAI_API_KEY` quando usar API e não houver login ChatGPT/Codex funcional.
- Endpoint/modelo atual não confirmado.
- Pedido depende de logo/rosto/produto real e a referência não foi fornecida/localizada.
