---
name: imagen
description: Route AI image/video generation with cost guards.
version: 0.1.0
author: Henri Claude Le Bourlegat, Claude Arcanjuz
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [image-generation, video-generation, onepassword, open-design]
    related_skills: [open-design-marketing-production]
---

# /imagen Skill

Use esta skill quando Henri, Miguel, Vince ou outro agente Arcanjuz pedir `/imagen`, geração de imagem, edição de imagem, thumbnail, mockup visual, storyboard, vídeo curto, animação ou mídia para Open Design.

A skill não guarda segredo e não inventa credenciais. Chaves ficam no 1Password e só entram no processo de execução via `op read` ou variáveis de ambiente temporárias.

## Quando usar

- `/imagen <pedido>` para imagem, edição de imagem, referência visual, variação ou thumbnail **quando a rota ainda deve ser decidida por custo/qualidade/risco**.
- `/imagen video <pedido>` para vídeo, animação de frame, product shot em movimento ou clipe de campanha, sempre com avaliação de custo antes de executar geração paga.
- `/imagen-gpt <pedido>` quando Henri já decidiu usar ChatGPT/OpenAI Images.
- `/imagen-google <pedido>` quando Henri já decidiu usar Google AI / Gemini / Imagen / Veo.
- `/imagen-kie <pedido>` quando Henri já decidiu usar Kie.AI / Kling / Seedance / modelos hospedados ali.
- Assets para Open Design, landings, App CCIA, CRESCER, Cazco ou materiais premium.
- Conversão de briefing em prompt + avaliação de custo + geração + salvamento + log lateral.

Não use para publicar produção sem aprovação explícita de Henri.

## Princípios obrigatórios

1. **Segredos no 1Password.** Nunca cole chaves no chat, repo, skill, segundo-cérebro ou arquivo de log.
2. **Referência real.** Nunca descreva logo, rosto, identidade visual ou produto em palavras se houver arquivo real. Use o arquivo como referência.
3. **Custo antes de vídeo.** Antes de qualquer vídeo pago: declarar fornecedor, modelo, duração, resolução, estimativa em USD/créditos e aguardar OK explícito. Um OK cobre uma execução.
4. **Rascunho barato primeiro.** Para imagem, gere rascunho barato antes de modelo premium, salvo pedido explícito de qualidade final.
5. **Pasta plana.** Salve mídia final em uma única pasta `geracoes/`, sem subpastas, com referências em `geracoes/refs/`.
6. **Log lateral.** Para cada arquivo salvo, escreva JSON de mesmo nome-base com prompt, fornecedor, modelo, refs, parâmetros, custo estimado e data.
7. **Open Design.** Quando for para Open Design, salve também ou copie o asset para `assets/imagen/` do projeto e registre a origem.

## Pré-requisitos

### 1Password

Use `op` como fonte canônica de segredos:

```bash
op whoami
op read "op://<vault>/<item>/<field>"
```

Se o caminho do item não estiver configurado, pare e peça a Henri/Miguel o caminho 1Password. Não liste nem leia segredos desnecessários.

### Variáveis temporárias esperadas

- `KIE_API_KEY` — Kie.AI.
- `GOOGLE_API_KEY` ou `GEMINI_API_KEY` — Google AI Studio / Gemini / Imagen / Veo.
- `OPENAI_API_KEY` — OpenAI Images API, quando usar API.
- Login ChatGPT/Codex — quando usar geração integrada ao Codex/ChatGPT em vez de OpenAI API.

Sugestão de sessão, sem persistir segredos:

```bash
export KIE_API_KEY="$(op read 'op://<vault>/Kie.AI/credencial')"
export GOOGLE_API_KEY="$(op read 'op://Miguel/Google Gemini API/credencial')"
export OPENAI_API_KEY="$(op read 'op://Miguel/OpenAI API Key/credencial')"
```

## Comandos e roteamento

### `/imagen <pedido>` — decisão assistida por custo

Use `/imagen` quando Henri ainda não escolheu fornecedor. Antes de gerar, faça uma **avaliação curta de custo x qualidade x risco** e recomende uma rota.

Formato obrigatório antes da execução:

```text
Avaliação /imagen
Pedido: <resumo>
Rotas viáveis:
1. <fornecedor/modelo> — custo estimado: <USD/créditos/faixa ou “incluído na assinatura”>; qualidade: <baixa|média|alta>; risco: <texto/ref/latência>; uso recomendado: <quando>
2. ...
Recomendação: <rota> porque <motivo direto>.
Execução: posso gerar agora por <rota>? 
```

Regras:

- Para **imagem paga ou com custo incerto**, informe estimativa/faixa antes de executar.
- Para **vídeo pago**, sempre aguarde OK explícito antes de criar task.
- Para **imagem barata/baixa materialidade**, pode recomendar e executar se Henri já deu comando imperativo claro, mas ainda registre custo estimado no JSON lateral.
- Se preço atual do fornecedor não estiver conhecido, consulte documentação/painel atual ou marque como “custo a confirmar” e não invente valor.
- Não transforme `/imagen` em pergunta “quer Gemini?”; compare rotas e dê recomendação operacional.

### Comandos de rota direta

Use estes apenas quando Henri já tem a rota clara:

- `/imagen-gpt <pedido>` — força ChatGPT/OpenAI Images. Não comparar rotas salvo risco/custo anormal.
- `/imagen-google <pedido>` — força Google AI / Gemini / Imagen / Veo. Não comparar rotas salvo risco/custo anormal.
- `/imagen-kie <pedido>` — força Kie.AI / Kling / Seedance / modelo hospedado. Para vídeo, cotar e aguardar OK.

## Roteamento padrão

**Não existe fornecedor único padrão.** A skill deve escolher a rota pelo objetivo do asset, custo, disponibilidade de credencial e preferência explícita de Henri. Não force Google Gemini/Imagen quando o pedido não pedir Google.

Regra prática:

- Se Henri usar `/imagen-gpt`, `/imagen-google` ou `/imagen-kie`, respeite a rota direta.
- Se Henri usar `/imagen`, compare rotas viáveis com estimativa de custo antes da execução.
- Se Henri nomear um fornecedor/modelo no texto, use esse fornecedor/modelo ou pare se credencial/modelo faltar.
- Se Henri pedir imagem final premium, texto legível, UI, campanha, embalagem ou peça com copy: recomende ChatGPT/OpenAI Images, mostrando custo estimado.
- Se Henri pedir rascunho barato/rápido ou variações exploratórias sem texto crítico: recomende Google AI Gemini/Imagen, mostrando custo estimado.
- Se Henri pedir vídeo, motion, Kling/Seedance ou modelo hospedado: recomende Kie.AI ou Veo conforme custo/qualidade, com aprovação antes de custo pago.

| Pedido | Rota provável | Alternativa | Critério de decisão |
|---|---|---|---|
| Imagem final premium / campanha | ChatGPT/OpenAI Images | Google AI | Qualidade e direção criativa > menor custo. |
| Imagem com texto legível | ChatGPT/OpenAI Images | Google AI | Legibilidade e fidelidade de copy. |
| UI/mockup/app screen | Open Design ou ChatGPT/OpenAI Images | Google AI | Editabilidade se protótipo; imagem se asset final. |
| Imagem rascunho barato | Google AI Gemini/Imagen | ChatGPT/OpenAI Images | Custo/velocidade > refinamento. |
| Imagem com refs fortes | ChatGPT/OpenAI Images ou Google AI | Kie.AI se hospedar modelo adequado | Qual suporte real a referência no endpoint atual. |
| Vídeo padrão | Kie.AI Kling/Seedance | Google Veo | Custo, duração, resolução, disponibilidade. |
| Vídeo premium | Google Veo | Kie.AI modelo pro | Qualidade final e orçamento aprovado. |
| Open Design asset | Modelo conforme tarefa | — | Salvar em `assets/imagen/` + log. |

Se a rota escolhida falhar por limite, indisponibilidade ou modelo ausente, cair para a segunda rota e registrar o motivo. Se falhar por autenticação, parar e avisar.

## Estrutura de arquivos

Escolha uma pasta estável por workspace/projeto:

```text
<workspace>/
├── geracoes/
│   ├── refs/
│   ├── projeto_descricao_YYYYMMDD-HHMMSS.png
│   └── projeto_descricao_YYYYMMDD-HHMMSS.json
└── .imagen/
    └── providers.local.json   # opcional: caminhos 1Password, sem segredos
```

Nomeação:

```text
{projeto}_{descricao}_{YYYYMMDD-HHMMSS}.{png|jpg|webp|mp4}
```

## Procedimento

1. **Classificar o pedido.** Identifique tipo: imagem, edição, variação, vídeo ou asset Open Design. Critério: uma rota inicial escolhida.
2. **Coletar refs.** Verifique arquivos reais de logo/rosto/produto/estilo. Critério: todos os assets sensíveis existem ou o processo parou pedindo referência.
3. **Resolver credenciais.** Confirme `op whoami` ou env temporária. Critério: variável necessária presente apenas no processo.
4. **Cotar.** Para `/imagen`, sempre apresentar avaliação comparativa de custo/qualidade/risco antes da rota final. Para `/imagen-gpt`, `/imagen-google` e `/imagen-kie`, cotar apenas a rota escolhida e alertar se houver risco/custo anormal. Para vídeo, calcular custo antes de executar e aguardar aprovação explícita. Critério: custo estimado registrado; vídeo pago aprovado antes da task.
5. **Gerar.** Chame a ficha do fornecedor em `references/`. Critério: arquivo final baixado localmente.
6. **Registrar.** Escreva JSON lateral. Critério: `.json` válido ao lado da mídia.
7. **Verificar.** Abra/inspecione dimensões, tamanho e, quando visual importa, use `vision_analyze` ou screenshot. Critério: arquivo não corrompido e coerente com briefing.
8. **Disponibilizar.** Entregue mídia e caminho. Para Open Design, copie para o projeto e informe path interno.

## Log lateral obrigatório

```json
{
  "skill": "imagen",
  "pedido": "texto original do usuário",
  "fornecedor": "kie.ai|google-ai|chatgpt|openai",
  "modelo": "id do modelo",
  "prompt": "prompt enviado",
  "refs": ["geracoes/refs/logo.png"],
  "params": {"aspect_ratio":"16:9","resolution":"1024x1024"},
  "custo_estimado_usd": 0.05,
  "status": "ok",
  "criado_em": "2026-08-18T00:00:00Z"
}
```

## Fichas rápidas

Leia as referências antes de executar:

- `references/kie-ai.md` — Kie.AI para vídeo/modelos hospedados.
- `references/google-ai.md` — Google AI Studio, Gemini/Imagen/Veo.
- `references/chatgpt-openai.md` — ChatGPT/Codex image_gen e OpenAI Images API.
- `references/open-design.md` — integração com projetos Open Design.
- `templates/providers.local.json` — mapa local de caminhos 1Password, sem segredos.

## Nota Open Design — skill não é connector

Esta skill aparece em Open Design como **skill/recipe**, não como `connector` de projeto. Portanto, `connectors: []` não significa que a skill esteja ausente. Connectors são integrações externas como Composio/Canva/GitHub; `/imagen`, `/imagen-gpt`, `/imagen-google` e `/imagen-kie` são rotas operacionais/skills.

Se a geração raster pelo fornecedor não estiver disponível dentro do agente Open Design, use o fallback correto: gerar pelo Hermes `/imagen*` fora do Open Design, salvar o arquivo localmente, copiar para `assets/imagen/` do projeto Open Design e registrar JSON lateral. Não invente que `@imagen-gpt` é um conector.

## Pitfalls

- Não grave `export ...` em `.bashrc`, `.env`, repo ou log de projeto.
- URLs temporárias de mídia expiram; baixe imediatamente.
- Trabalhos de vídeo são assíncronos; limite polling a 10 minutos salvo instrução diferente.
- Não execute várias gerações pagas em paralelo sem aprovação e limite de custo.
- Se o modelo ou endpoint mudou, consulte a documentação atual do fornecedor antes de insistir.

## Verificação final

Antes de responder sucesso:

- [ ] arquivo de mídia existe e tem tamanho maior que zero;
- [ ] JSON lateral existe e é JSON válido;
- [ ] nenhum segredo foi escrito em arquivo/log;
- [ ] fornecedor/modelo/custo foram reportados;
- [ ] se Open Design: arquivo existe no projeto em `assets/imagen/` ou artifact equivalente;
- [ ] se vídeo: duração/resolução foram verificadas com ferramenta de mídia quando disponível.
