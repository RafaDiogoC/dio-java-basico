pip install azure-ai-textanalytics azure-cognitiveservices-speech
pip install azure-ai-textanalytics azure-cognitiveservices-speech
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential
import json

# 🔹 Substitua com suas credenciais do Azure
AZURE_LANGUAGE_KEY = "SUA_CHAVE"
AZURE_LANGUAGE_ENDPOINT = "SEU_ENDPOINT"

# Configuração do cliente
def authenticate_client():
    return TextAnalyticsClient(endpoint=AZURE_LANGUAGE_ENDPOINT, credential=AzureKeyCredential(AZURE_LANGUAGE_KEY))

client = authenticate_client()

# Lendo frases do arquivo
with open("inputs/sentences.txt", "r", encoding="utf-8") as file:
    sentences = [line.strip() for line in file.readlines()]

# Analisando texto
response = client.analyze_sentiment(documents=sentences)

# Salvando resultados
results = []
for idx, doc in enumerate(response):
    results.append({
        "Texto": sentences[idx],
        "Sentimento": doc.sentiment,
        "Confiança": {
            "Positivo": doc.confidence_scores.positive,
            "Neutro": doc.confidence_scores.neutral,
            "Negativo": doc.confidence_scores.negative,
        }
    })

# Escrevendo saída JSON
with open("outputs/analysis_results.json", "w", encoding="utf-8") as output_file:
    json.dump(results, output_file, indent=4, ensure_ascii=False)

print("✅ Análise de texto concluída! Resultados salvos em outputs/analysis_results.json")
import azure.cognitiveservices.speech as speechsdk

# 🔹 Substitua com suas credenciais do Azure
AZURE_SPEECH_KEY = "SUA_CHAVE"
AZURE_SPEECH_REGION = "SUA_REGIAO"

# Inicializando serviço de fala
speech_config = speechsdk.SpeechConfig(subscription=AZURE_SPEECH_KEY, region=AZURE_SPEECH_REGION)
speech_config.speech_synthesis_voice_name = "pt-BR-FranciscaNeural"

# Entrada de texto
text = "Olá! Este é um teste de conversão de texto em fala com o Azure Speech Studio."

# Configuração do sintetizador
speech_synthesizer = speechsdk.SpeechSynthesizer(speech_config=speech_config)

# Convertendo texto para fala
speech_synthesizer.speak_text_async(text).get()
print("✅ Conversão de texto em fala concluída!")
import azure.cognitiveservices.speech as speechsdk

# 🔹 Substitua com suas credenciais do Azure
AZURE_SPEECH_KEY = "SUA_CHAVE"
AZURE_SPEECH_REGION = "SUA_REGIAO"

# Inicializando serviço de fala
speech_config = speechsdk.SpeechConfig(subscription=AZURE_SPEECH_KEY, region=AZURE_SPEECH_REGION)
speech_config.speech_synthesis_voice_name = "pt-BR-FranciscaNeural"

# Entrada de texto
text = "Olá! Este é um teste de conversão de texto em fala com o Azure Speech Studio."

# Configuração do sintetizador
speech_synthesizer = speechsdk.SpeechSynthesizer(speech_config=speech_config)

# Convertendo texto para fala
speech_synthesizer.speak_text_async(text).get()
print("✅ Conversão de texto em fala concluída!")
import azure.cognitiveservices.speech as speechsdk

# 🔹 Substitua com suas credenciais do Azure
AZURE_SPEECH_KEY = "SUA_CHAVE"
AZURE_SPEECH_REGION = "SUA_REGIAO"

# Configurando serviço de reconhecimento de fala
speech_config = speechsdk.SpeechConfig(subscription=AZURE_SPEECH_KEY, region=AZURE_SPEECH_REGION)
speech_recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config, language="pt-BR")

print("🎤 Fale algo...")
result = speech_recognizer.recognize_once()

if result.reason == speechsdk.ResultReason.RecognizedSpeech:
    print(f"✅ Texto reconhecido: {result.text}")
elif result.reason == speechsdk.ResultReason.NoMatch:
    print("🚨 Nenhuma fala reconhecida.")
elif result.reason == speechsdk.ResultReason.Canceled:
    print(f"🚨 Erro: {result.cancellation_details.reason}")
# 🚀 Projeto de Análise de Texto e Fala com Azure AI

## 📌 Descrição
Este projeto demonstra como utilizar os serviços **Azure Speech Studio** e **Language Studio** para:
- 🔹 Analisar textos (detecção de sentimentos, extração de frases-chave).
- 🔹 Converter texto em fala usando **Azure Speech Studio**.
- 🔹 Transcrever áudio para texto usando **reconhecimento de fala**.

## 📂 Estrutura do Repositório
📂 **inputs/** → Contém frases para análise.  
📂 **outputs/** → Guarda os resultados da análise.  
📜 **text_analysis.py** → Código para análise de texto.  
📜 **text_to_speech.py** → Código para converter texto em fala.  
📜 **speech_to_text.py** → Código para transcrição de áudio.  

## 🎯 Como Executar
1. Instale as dependências:
   ```bash
   pip install azure-ai-textanalytics azure-cognitiveservices-speech

---

### **Passo 4: Publicar no GitHub e Entregar**
Agora, publique seu projeto no **GitHub**:
```bash
git init
git add .
git commit -m "Projeto Azure AI concluído"
git branch -M main
git remote add origin https://github.com/seu-usuario/azure-ai-project.git
git push -u origin main
