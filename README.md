# ia-generativa-openai
IA Generativa Openai

import pandas as pd

df = pd.read_csv('usuarios.csv')
user_ids = df['UserID'].tolist()
print(user_ids)

import requests
import json

def get_user(id):
  response = requests.get(f'{sdw2023_api_url}/users/{id}')
  return response.json() if response.status_code == 200 else None

users = [user for id in user_ids if (user := get_user(id)) is not None]
print(json.dumps(users, indent=2))

},
    "card": {
      "id": 4991,
      "number": "8965 0987 2431 8964",
      "limit": 1000.0
    },
    "features": [],
    "news": []
  },
  {
    "id": 5133,
    "name": "Anamara",
    "account": {
      "id": 5459,
      "number": "00074-2",
      "agency": "0003",
      "balance": 0.0,
      "limit": 500.0
    },
    "card": {
      "id": 4992,
      "number": "3901 1487 2064 2945",
      "limit": 1000.0
    },
    "features": [],
    "news": [
      {
        "id": 9613,
        "icon": "https://digitalinnovationone.github.io/santander-dev-week-2023-api/icons/credit.svg",
        "description": "Invista hoje, garanta o seu futuro!"
      },
      {
        "id": 9614,
        "icon": "https://digitalinnovationone.github.io/santander-dev-week-2023-api/icons/credit.svg",
        "description": "Anamara, invista hoje e garanta um futuro pr\u00f3spero! \ud83d\udcb0\n\nAnamara, sua seguran\u00e7a financeira come\u00e7a com investimentos inteligentes.\ud83d\udcbc\n\nAnamara, invista agora e realize seus sonhos! \ud83c\udf1f"
      }
    ]
  },
  {
    "id": 5134,
    "name": "Louise",
    "account": {
      "id": 5460,
      "number": "00023-4",
      "agency": "0004",
      "balance": 0.0,
      "limit": 500.0
    },
    "card": {
      "id": 4993,
      "number": "4684 4678 7894 3953",
      "limit": 1000.0
    },
    "features": [],
    "news": []
  }
]


!pip install openai

# @title
# Documentação Oficial da API OpenAI: https://platform.openai.com/docs/api-reference/introduction
# Informações sobre o Período Gratuito: https://help.openai.com/en/articles/4936830

# Para gerar uma API Key:
# 1. Crie uma conta na OpenAI
# 2. Acesse a seção "API Keys"
# 3. Clique em "Create API Key"
# Link direto: https://platform.openai.com/account/api-keys

# Substitua o texto TODO por sua API Key da OpenAI, ela será salva como uma variável de ambiente.
openai_api_key = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'

import openai

openai.api_key = openai_api_key

def generate_ai_news(user):
  completion = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
      {
          "role": "system",
          "content": "Você é um especialista em finanças."
      },
      {
          "role": "user",
          "content": f"Crie opções de investimento mediante limite de crédico para {user['name']} informando o que ele deve fazer para aumentar seu dinheiro(máximo de 100 caracteres)"
      }
    ]
  )
  return completion.choices[0].message.content.strip('\"')

for user in users:
  news = generate_ai_news(user)
  print(news)
  user['news'].append({
      "icon": "https://digitalinnovationone.github.io/santander-dev-week-2023-api/icons/credit.svg",
      "description": news
  })

  Invista em ações de empresas de tecnologia em crescimento.
Opções: Renda fixa, Fundos de investimento, Diversificar carteira, Estudar e buscar conhecimento financeiro.
1. Ações: Pesquise empresas sólidas e invista com sabedoria.
2. Fundos de investimento: Diversifique seus investimentos para mitigar os riscos.
3. Imóveis: Compre propriedades para valorização ao longo do tempo.
4. Tesouro Direto: Invista em títulos públicos para rendimentos seguros.
5. Economize e evite dívidas: Corte gastos e priorize o pagamento de suas dívidas.
6. Empreenda: Considere abrir seu próprio negócio para aumentar sua renda.
7. Educação financeira: Busque conhecimento e tome decisões informadas.
8. Considere investir em criptomoedas: Avalie o mercado e invista com cautela.
9. Previdência privada: Planeje seu futuro e faça aportes regularmente.
10. Consulte um especialista: Busque orientação profissional para personalizar sua estratégia.
Invista em ações diversificadas de longo prazo.

def update_user(user):
  response = requests.put(f"{sdw2023_api_url}/users/{user['id']}", json=user)
  return True if response.status_code == 200 else False

for user in users:
  success = update_user(user)
  print(f"User {user['name']} updated? {success}!")

  User Diego updated? True!
User Rosana updated? True!
User Anamara updated? True!
User Louise updated? True!
