# Kie.AI provider card for /imagen

Use Kie.AI principalmente para vídeo ou modelos multimodais hospedados ali quando for a rota capaz mais barata.

## Autenticação

Variável temporária: `KIE_API_KEY`.

```bash
export KIE_API_KEY="$(op read 'op://<vault>/Kie.AI/credencial')"
```

Cabeçalho típico:

```http
Authorization: Bearer $KIE_API_KEY
Content-Type: application/json
```

## Procedimento

1. Conferir documentação atual do modelo no painel Kie.AI.
2. Montar JSON com prompt, duração, proporção, resolução e URLs/arquivos de referência conforme a doc.
3. Criar task.
4. Poll de status a cada 10–15s, no máximo 10 min.
5. Baixar a mídia assim que o status concluir.
6. Salvar mídia + JSON lateral.

## Regras

- Erro de autenticação: pare, não tente fallback silencioso.
- Erro de modelo inexistente: verificar ID atual na documentação.
- Vídeo pago: cotar e esperar OK explícito antes de criar task.
