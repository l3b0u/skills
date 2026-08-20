# ChatGPT / OpenAI provider card for /imagen

Use ChatGPT/OpenAI quando o pedido precisa de texto dentro da imagem, UI legível, cartazes, embalagem, ou quando Henri preferir usar assinatura/login ChatGPT em vez de créditos de outro fornecedor.

## Modos suportados

### 1. ChatGPT/Codex image generation

Se `codex` estiver autenticado e tiver ferramenta de imagem disponível, pode gerar via login ChatGPT/Codex sem expor API key no processo.

Verificações:

```bash
codex --version
codex login status
```

Regra: salve o arquivo no caminho combinado e não misture fontes de imagem no mesmo lote se a consistência visual for crítica.

### 2. OpenAI Images API

Variável temporária: `OPENAI_API_KEY`.

```bash
export OPENAI_API_KEY="$(op read 'op://Miguel/OpenAI API Key/credencial')"
```

Use endpoint/SDK atual da OpenAI Images API. Não fixar ID antigo se a documentação mudou; registrar o ID real usado no JSON lateral.

## Regras

- Melhor rota para texto legível em imagem.
- Para edição com logo/rosto, usar arquivo real como input/reference.
- Não registrar payload com base64 gigante no log lateral; registre caminho local da referência.
