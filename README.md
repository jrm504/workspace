
# Hermes Agent profiles

## Install distribution profiles

```bash
hermes profile install profiles/architect --name architect --alias --force
hermes profile install profiles/ba --name ba --alias --force
hermes profile install profiles/contract --name contract --alias --force
hermes profile install profiles/developer --name developer --alias --force
hermes profile install profiles/tester --name tester --alias --force
hermes profile install profiles/orchestrator --name orchestrator --alias --force
hermes profile install profiles/po --name po --alias --force
hermes profile install profiles/qa --name qa --alias --force
hermes profile install profiles/reviewer --name reviewer --alias --force
hermes profile install profiles/docs-writer --name docs-writer --alias --force
hermes profile install profiles/security --name security --alias --force
```

## Update distribution profiles

```bash
hermes profile update architect --force-config --yes
hermes profile update ba --force-config --yes
hermes profile update contract --force-config --yes
hermes profile update developer --force-config --yes
hermes profile update orchestrator --force-config --yes
hermes profile update po --force-config --yes
hermes profile update qa --force-config --yes
hermes profile update reviewer --force-config --yes
hermes profile update security --force-config --yes
hermes profile update tester --force-config --yes
hermes profile update docs-writer --force-config --yes
```

## Remove old Docker containers

```bash
docker ps -aq --filter 'name=hermes' | xargs -r docker rm -f
```

## Kanban Board

```bash
hermes kanban boards create vnbrokers \
        --name "VNBrokers" \
        --description "Multi-agent development board for VNBrokers" \
        --switch
```

## Useful commands

```bash
hermes -p contract skills list --source builtin
hermes profile delete contract --yes
```

```bash
HERMES_CA_BUNDLE=${HOME}/certs/internal-rootca-bundle.pem
SSL_CERT_FILE=${HOME}/certs/internal-rootca-bundle.pem
```

Remove the old deleted profiles in `~/.hermes/profiles/.deleted/*` before re-installing the distribution profile.

```bash
rm ~/.hermes/profiles/.deleted/*
```

References:

- [Hermes configuration](https://github.com/NousResearch/hermes-agent/blob/main/hermes_cli/config_defaults.py)
