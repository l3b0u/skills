# Google AI provider card for /imagen

Use Google AI para Gemini/Imagen em imagem e Veo em vídeo quando for a melhor relação qualidade/custo.

## Autenticação

Variáveis temporárias: `GOOGLE_API_KEY` ou `GEMINI_API_KEY`.

```bash
export GOOGLE_API_KEY="$(op read 'op://Miguel/Google Gemini API/credencial')"
```

O padrão Google AI Studio normalmente usa a chave no parâmetro `?key=` ou SDK oficial. Não grave a chave em URL persistida ou log.

## Imagem

- Bom para rascunhos baratos, variações e imagem com referência.
- Sempre passar arquivos reais para logos/rostos/produtos quando houver.
- Confirmar ID de modelo atual antes de chamar.

## Vídeo / Veo

- Tratar como geração paga e geralmente assíncrona.
- Declarar duração, resolução, amostras e custo estimado antes da execução.
- Poll com limite e baixar resultado imediatamente.

## Regras

- Não enviar segredo em arquivo de prompt.
- Se o SDK imprimir request completa com chave, interromper e limpar logs antes de prosseguir.
