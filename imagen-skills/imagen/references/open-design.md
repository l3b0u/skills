# Open Design integration for /imagen

Use quando a geração será consumida por um projeto Open Design.

## Padrão de saída

1. Gerar em `geracoes/` primeiro.
2. Copiar a mídia aprovada para o projeto em:

```text
assets/imagen/{nome-do-arquivo}
assets/imagen/{nome-do-arquivo-base}.json
```

3. Em HTML/CSS/TSX do Open Design, referenciar com path absoluto do projeto quando o preview quebrar paths relativos.
4. Registrar no JSON lateral o projeto e o arquivo Open Design.

## Manifesto mínimo

```json
{
  "open_design": {
    "project": "<project-id>",
    "asset_path": "assets/imagen/arquivo.png",
    "used_in": ["index.html"]
  }
}
```

## Regras

- Não publicar externamente sem aprovação de Henri.
- Não recriar logos; usar identidade oficial.
- Para CRESCER/App CCIA, manter visual premium, sem estética genérica de IA.
