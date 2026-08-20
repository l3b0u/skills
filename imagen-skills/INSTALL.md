# Instalação — skills /imagen

Este pacote contém:

- `imagen`
- `imagen-gpt`
- `imagen-google`
- `imagen-kie`

## Instalação por cópia

No perfil Hermes de destino, extraia dentro da pasta de skills do perfil.

### Perfil padrão

```bash
mkdir -p ~/.hermes/skills/media
tar -xzf imagen-skills-20260818.tar.gz -C ~/.hermes/skills/media/
hermes skills list | grep imagen
```

### Perfil nomeado

Troque `<perfil>` pelo nome real:

```bash
mkdir -p ~/.hermes/profiles/<perfil>/skills/media
tar -xzf imagen-skills-20260818.tar.gz -C ~/.hermes/profiles/<perfil>/skills/media/
hermes --profile <perfil> skills list | grep imagen
```

## Depois de instalar

Não use `/reload-skills` como passo obrigatório.

Opção segura e universal:

1. Feche a sessão atual ou abra uma nova conversa.
2. Rode `hermes skills list | grep imagen` para verificar.
3. Se estiver em um perfil nomeado, use `hermes --profile <perfil> skills list | grep imagen`.

Em algumas versões/superfícies do Hermes existe `/reload-skills`, mas não conte com ele em Desktop/Gateway. Nova sessão sempre recarrega as skills.
