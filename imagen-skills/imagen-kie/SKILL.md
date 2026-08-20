---
name: imagen-kie
description: Use when /imagen-kie should force Kie route.
version: 0.1.0
author: Henri Claude Le Bourlegat, Claude Arcanjuz
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [image-generation, video-generation, kie-ai, kling, seedance, cost-guard]
    related_skills: [imagen]
---

# /imagen-kie Skill

## When to Use

Use esta skill quando Henri pedir `/imagen-kie <pedido>` ou disser explicitamente que quer usar Kie.AI, Kling, Seedance ou modelo hospedado ali.

## Regra principal

Esta é uma rota direta: **não compare fornecedores por padrão**. Use Kie.AI, salvo se houver bloqueio de credencial, custo anormal, modelo indisponível ou risco técnico relevante.

## Procedimento

1. Carregue também a skill `imagen` e siga as regras gerais de segurança, arquivos, referências reais, log lateral e verificação.
2. Na skill `imagen`, carregue a ficha de Kie.AI antes de executar.
3. Confirme `KIE_API_KEY` via variável temporária/op; não gravar chaves.
4. Antes de qualquer geração paga — especialmente vídeo — declarar modelo, duração, resolução, quantidade de samples, custo estimado em USD/créditos e aguardar OK explícito.
5. Criar task, fazer polling limitado, baixar mídia imediatamente e salvar JSON lateral.
6. Salve mídia + JSON lateral com `fornecedor: "kie.ai"` e o modelo real usado.

## Nota Open Design — skill não é connector

Esta skill aparece em Open Design como **skill/recipe**, não como `connector` de projeto. Portanto, `connectors: []` não significa que a skill esteja ausente. Connectors são integrações externas como Composio/Canva/GitHub; `/imagen-kie` é uma rota operacional/skill.

Se a geração raster/vídeo pela Kie.AI não estiver disponível dentro do agente Open Design, use o fallback correto: gerar pelo Hermes `/imagen-kie` fora do Open Design, salvar o arquivo localmente, copiar para `assets/imagen/` do projeto Open Design e registrar JSON lateral. Não invente que `@imagen-kie` é um conector.

## Quando parar

- Credencial Kie.AI ausente ou inválida.
- Modelo/endpoint atual não confirmado no painel/documentação.
- Vídeo ou task paga sem OK explícito de Henri.
