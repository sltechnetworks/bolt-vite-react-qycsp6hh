# API Backend - Lavanderia 60 Minutos

Sistema backend em Node.js para integração com a API da Lavanderia 60 Minutos.

## Funcionalidades Implementadas

1. **Integração com APIs**
   - Consumo da API de lojas (`/stores/all`)
   - Consumo da API de monitoramento (`/stores_monitoring/list`)
   - Combinação dos dados em uma única resposta

2. **Dados por Loja**
   - Código da loja
   - Estado (extraído do código)
   - Links do Blynk:
     - Power ON: Ligar equipamento
     - Power OFF: Desligar equipamento
     - Status: Verificar conexão do hardware
   - Monitoramento:
     - Múltiplos erros por loja
     - Status do erro
     - Tipo do erro
     - Data de criação

3. **Recursos Técnicos**
   - Cache opcional com Redis
   - Tratamento de erros centralizado
   - Logs estruturados
   - Rate limiting para proteção da API
   - Compressão de resposta
   - Documentação Swagger

## Endpoints

### GET `/api/stores`
Retorna todas as lojas com seus dados de monitoramento e links do Blynk.

Exemplo de resposta:
```json
{
  "status": "success",
  "data": [
    {
      "code": "SP40",
      "state": "SP",
      "blynk_power_on": "https://ny3.blynk.cloud/external/api/update?token=xxx&pin=V57&value=1",
      "blynk_power_off": "https://ny3.blynk.cloud/external/api/update?token=xxx&pin=V57&value=0",
      "blynk_status": "https://ny3.blynk.cloud/external/api/isHardwareConnected?token=xxx",
      "monitoring": [
        {
          "id": "618d1872-...",
          "attributes": {
            "store_code": "SP40",
            "status": "unresolved",
            "error_type": "system",
            "created_at": "2024-11-15T09:45:21.353-03:00"
          }
        }
      ]
    }
  ],
  "totalStores": 570,
  "lastUpdate": "2024-12-10T13:00:00.000Z"
}
```

### GET `/api/stores/:code`
Retorna os dados de uma loja específica pelo código.

## Instalação e Uso

1. Instale as dependências:
```bash
npm install
```

2. Configure as variáveis de ambiente:
```bash
cp .env.example .env
```

3. Execute o servidor:
```bash
npm run dev
```

## Estrutura do Projeto

```
src/
  ├── controllers/     # Controladores
  ├── middlewares/    # Middlewares
  ├── routes/         # Rotas
  ├── services/       # Serviços
  └── validators/     # Validadores
```

## Tecnologias Utilizadas

- Node.js
- Express.js
- Axios para requisições HTTP
- Redis para cache (opcional)
- Winston para logs
- Yup para validação
- Swagger para documentação