# Análise de Sentimentos com Language Studio no Azure AI

## Visão Geral
Este guia explica como implementar uma solução de análise de sentimentos utilizando o Azure AI Language Studio, parte dos serviços cognitivos da Microsoft Azure.

## Pré-requisitos
- [Conta Azure](https://azure.microsoft.com/free/)
- Acesso ao [Azure Portal](https://portal.azure.com)
- Assinatura com acesso ao Azure AI Services

## Configuração Inicial

### 1. Criar um Recurso de Language Service
1. No Azure Portal, clique em "Criar um recurso"
2. Pesquise por "Language Service"
3. Selecione e configure:
   - **Nome do recurso**: (ex: sentiment-analysis-01)
   - **Região**: Selecione a mais próxima
   - **Tipo de preço**: F (Free) para testes
4. Clique em "Revisar + criar" e confirme

### 2. Acessar o Language Studio
1. Vá para [Language Studio](https://language.cognitive.azure.com/)
2. Conecte-se usando sua conta Azure
3. Selecione o recurso criado

## Implementando Análise de Sentimentos

### 1. Criar um Projeto
1. No Language Studio, selecione "Custom text classification"
2. Clique em "Create new project"
3. Configure:
   - **Nome do projeto**: AnaliseSentimentos
   - **Descrição**: Análise de sentimentos em avaliações de clientes
   - **Tipo de projeto**: Sentiment Analysis

### 2. Carregar Dados
1. Na seção "Data", clique em "Add data"
2. Opções de importação:
   - Upload de arquivos JSON/CSV
   - Conectar ao Azure Blob Storage
   - Inserir texto manualmente

### 3. Treinar o Modelo
1. Selecione os dados carregados
2. Clique em "Train"
3. Escolha o modelo base (recomendado: "prebuilt-sentiment")
4. Defina a divisão treino/teste (80/20 recomendado)
5. Inicie o treinamento

## Testando a Solução

### 1. Interface de Teste
1. Na seção "Deploy model", clique em "Test"
2. Insira textos para análise:
   - "Adorei o produto, entrega rápida!"
   - "Péssimo atendimento, nunca mais compro aqui."

### 2. Resultados Esperados
- **Sentimento**: Positivo/Neutro/Negativo
- **Confiança**: Score de 0-1
- **Entidades**: Palavras-chave identificadas

## Integração com Aplicações

### 1. Chamada via API REST
```python
import requests

endpoint = "https://[seu-endpoint].cognitiveservices.azure.com/"
headers = {
    "Ocp-Apim-Subscription-Key": "[SUA-CHAVE]",
    "Content-Type": "application/json"
}

data = {
    "documents": [
        {"id": "1", "text": "O serviço foi excelente!"}
    ]
}

response = requests.post(endpoint + "text/analytics/v3.0/sentiment", 
                        headers=headers, json=data)
print(response.json())


2. SDK Azure
python
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

credential = AzureKeyCredential("[SUA-CHAVE]")
client = TextAnalyticsClient(endpoint="[SEU-ENDPOINT]", credential=credential)

documents = ["Ótimo produto, recomendo!"]
response = client.analyze_sentiment(documents)
print(response[0].sentiment)
Melhores Práticas
✔️ Pré-processamento: Limpeza de texto (remoção de stopwords)
✔️ Avaliação contínua: Monitorar acurácia do modelo
✔️ Rotulagem cuidadosa: Garantir qualidade dos dados de treino
✔️ Versionamento: Manter diferentes versões do modelo

Limpeza de Recursos
Para evitar custos indesejados:

No Azure Portal, vá para o grupo de recursos

Selecione o recurso de Language Service

Clique em "Excluir"

Recursos Adicionais
Documentação Oficial

Exemplos de Código

Fórum de Suporte

text

Este README.md fornece um guia completo para implementação de análise de sentimentos usando o Azure AI Language Studio, desde a configuração inicial até a integração em aplicações.
New chat
Message DeepSeek
