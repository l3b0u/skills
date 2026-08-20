---
name: imagen-google
description: Use when /imagen-google should force Google route.
version: 0.1.0
author: Henri Claude Le Bourlegat, Claude Arcanjuz
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [image-generation, video-generation, google-ai, gemini, imagen, veo, cost-guard]
    related_skills: [imagen]
---

# /imagen-google Skill

## When to Use

Use esta skill quando Henri pedir `/imagen-google <pedido>` ou disser explicitamente que quer usar Google AI / Gemini / Imagen / Veo.

## Regra principal

Esta é uma rota direta: **não compare fornecedores por padrão**. Use Google AI, salvo se houver bloqueio de credencial, custo anormal, endpoint indisponível ou risco técnico relevante.

## Procedimento

1. Carregue também a skill `imagen` e siga as regras gerais de segurança, arquivos, referências reais, log lateral e verificação.
2. Na skill `imagen`, carregue a ficha de Google AI antes de executar.
3. Confirme `GOOGLE_API_KEY` ou `GEMINI_API_KEY` via variável temporária/op; não gravar chaves.
4. Antes de executar, informe custo estimado ou faixa da rota Google. Se preço atual não estiver conhecido, consulte documentação/painel atual ou marque como `custo a confirmar` e não invente valor.
5. Para Veo/vídeo: declarar fornecedor, modelo, duração, resolução, samples, custo estimado e aguardar OK explícito antes de criar task.
6. Salve mídia + JSON lateral com `fornecedor: "google-ai"` e o modelo real usado.

## Nota Open Design — skill não é connector

Esta skill aparece em Open Design como **skill/recipe**, não como `connector` de projeto. Portanto, `connectors: []` não significa que a skill esteja ausente. Connectors são integrações externas como Composio/Canva/GitHub; `/imagen-google` é uma rota operacional/skill.

Se a geração raster pelo Google AI não estiver disponível dentro do agente Open Design, use o fallback correto: gerar pelo Hermes `/imagen-google` fora do Open Design, salvar o arquivo localmente, copiar para `assets/imagen/` do projeto Open Design e registrar JSON lateral. Não invente que `@imagen-google` é um conector.

## Quando parar

- Credencial Google ausente ou inválida.
- Modelo/endpoint atual não confirmado.
- Vídeo pago sem OK explícito de Henri.
