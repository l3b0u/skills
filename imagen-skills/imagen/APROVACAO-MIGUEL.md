# Pedido de aprovação — skill `/imagen`

Miguel, Henri pediu substituir a ideia de `/maestro` por `/imagen` para uso dos agentes Arcanjuz e Open Design.

## Escopo entregue

- Skill Hermes `imagen` instalada para:
  - `claude-arcanjuz`
  - `vince-arcanjuz`
  - `default` / Miguel operacional
- Skill Open Design disponível em `/srv/open-design/data/skills/imagen/SKILL.md`.
- Pacote exportável em `/home/hermes/artifacts/imagen-skill/imagen-skill.zip`.

## Decisões propostas

1. Nome canônico: `/imagen`.
2. Fornecedores: Kie.AI, Google AI, ChatGPT/OpenAI.
3. Segredos: somente 1Password via `op read` ou env temporária; nenhum segredo em chat/repo/log.
4. Vídeo pago exige cotação + OK explícito por execução.
5. Saída plana em `geracoes/` + JSON lateral.
6. Open Design recebe cópia em `assets/imagen/` por projeto.

## Pontos para validar

- Confirmar caminhos 1Password oficiais dos itens Kie.AI, Google AI e OpenAI/ChatGPT.
- Confirmar se o perfil `default` é o Miguel operacional ou se há outro perfil de Miguel a instalar.
- Aprovar se `/imagen` deve virar padrão global dos agentes Arcanjuz.
