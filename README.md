# ETL - Extração de Dados de API

Este projeto é um script em Python que realiza um processo ETL (Extração, Transformação e Carga) a partir de uma API, utilizando a biblioteca `requests`.

## Requisitos

- Python 3.x
- Biblioteca `requests`
- Biblioteca `pandas`

## Instalação

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/etl-api.git
   cd etl-api
   ```

2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

## Uso

Execute o script principal para extrair os dados da API, transformá-los e salvá-los em um arquivo CSV:

```bash
python etl.py
```

O script realiza as seguintes etapas:
- Extrai os dados da API.
- Transforma os dados conforme necessário.
- Salva os dados processados em um arquivo CSV (`dados.csv`).

## Estrutura do Projeto

```
etl-api/
│-- etl.py
│-- config.json
│-- requirements.txt
│-- README.md
```

- `etl.py`: Script principal do ETL.
- `config.json`: Configuração da API.
- `requirements.txt`: Lista de dependências.
- `README.md`: Documentação do projeto.

## Exemplo de Código

```python
import requests
import pandas as pd
import json

# Carregar configuração
def load_config():
    with open("config.json", "r") as file:
        return json.load(file)

# Extrair dados da API
def extract():
    config = load_config()
    response = requests.get(config["api_url"], headers=config["headers"], params=config["params"])
    return response.json() if response.status_code == 200 else None

# Transformar dados
def transform(data):
    df = pd.DataFrame(data)
    return df

# Carregar dados

def load(df):
    df.to_csv("dados.csv", index=False)
    print("Dados salvos com sucesso!")

if __name__ == "__main__":
    data = extract()
    if data:
        df = transform(data)
        load(df)
    else:
        print("Erro na extração de dados.")
```

## Licença

Este projeto é distribuído sob a licença MIT.