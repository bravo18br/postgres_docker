# PostgreSQL Dockerized Server

Este projeto configura um servidor PostgreSQL utilizando contêineres Docker, com personalizações para timezone, configurações de conexão e armazenamento persistente.

## Recursos

- **Banco de Dados PostgreSQL:** Implementação completa do PostgreSQL com configurações padrão.
- **Timezone Personalizado:** Configurado para o fuso horário `America/Sao_Paulo` (UTC-3).
- **Volumes Persistentes:** Os dados do banco de dados são armazenados em volumes locais.
- **Configuração Personalizada:** Arquivos customizados, como `pg_hba.conf` e parâmetros do PostgreSQL, podem ser usados para ajustes específicos.
- **Healthcheck:** Verifica periodicamente a saúde do contêiner.

## Estrutura do Projeto

- **`docker-compose.yml`**: Configura o serviço PostgreSQL com parâmetros, volumes e redes.
- **`postgres_custom/`**: Diretório para configurações adicionais, como `pg_hba.conf` e `postgresql.conf`.

## Pré-requisitos

- Docker
- Docker Compose

## Configuração

### 1. Configurações do Docker Compose
- O arquivo `docker-compose.yml` está configurado com:
  - **Usuário:** `docker`
  - **Senha:** `docker`
  - **Banco de Dados Padrão:** `db`
  - **Porta Exposta:** `5432`

### 2. Configurações Customizadas
- Coloque seus arquivos customizados no diretório `postgres_custom`:
  - **`pg_hba.conf`**: Define métodos de autenticação e controle de acesso.
  - **`postgresql.conf`**: Ajuste configurações como conexões máximas, timeout de checkpoints, e muito mais.

### 3. Volume Persistente
- O volume `pg_data` armazena os dados do banco de forma persistente:
  ```yaml
  volumes:
    pg_data:
      driver: local
  ```

### 4. Rede
- Configurado para usar uma rede Docker `net` com driver `bridge`.

## Instalação

1. Clone o repositório:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd <NOME_DO_PROJETO>
   ```

2. Suba os contêineres:
   ```bash
   docker-compose up -d
   ```

3. Verifique o status:
   ```bash
   docker-compose ps
   ```

4. Teste a conexão:
   - Utilize ferramentas como `psql` ou clientes gráficos para conectar no PostgreSQL em [localhost:5432](localhost:5432).

## Configuração de Saúde

O contêiner possui um healthcheck configurado:
- **Comando:** Verifica a disponibilidade do PostgreSQL com `pg_isready`.
- **Intervalo:** 10 segundos.
- **Retries:** 3 tentativas antes de marcar o serviço como não saudável.

## Recursos Avançados

- **Escalabilidade:** Personalize o `docker-compose.yml` para incluir réplicas ou balanceadores de carga.
- **Integração:** Pode ser integrado com outros serviços como backend (Laravel, Node.js) e ferramentas de visualização (como Metabase ou Grafana).

## Suporte

Para dúvidas ou suporte, consulte a [documentação oficial do PostgreSQL](https://www.postgresql.org/docs/).

## Licença

Este projeto é licenciado sob a licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.
