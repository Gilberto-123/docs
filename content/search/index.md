

import telegram
from telegram.ext import Updater, CommandHandler
import pandas as pd

# Configurar o token do seu bot
bot_token = 'AAHDBQhXigtEbUS_jvNbqYsh2MVRLSSAmcQ'

# Configurar o chat_id para onde as mensagens serão enviadas
chat_id = 'http://t.me/Otre1_bot'

# Inicializar o bot
bot = telegram.Bot(token=bot_token)

# Função para enviar uma mensagem
def enviar_mensagem(texto):
    bot.send_message(chat_id=chat_id, text=texto)

# Simulação de dados de preços (substitua isso pelos dados reais)
data = {
    'Data': ['2023-01-01', '2023-01-02', '2023-01-03', '2023-01-04'],
    'Preço': [100, 105, 98, 110]
}

# Converter os dados para um DataFrame
df = pd.DataFrame(data)

# Calcular médias móveis (exemplo simples)
df['MA_10'] = df['Preço'].rolling(window=10).mean()
df['MA_20'] = df['Preço'].rolling(window=20).mean()

# Verificar cruzamento de médias móveis
if df['MA_10'].iloc[-1] > df['MA_20'].iloc[-1]:
    enviar_mensagem('Sinal de COMPRA: Cruzamento de MA de cima para baixo')
elif df['MA_10'].iloc[-1] < df['MA_20'].iloc[-1]:
    enviar_mensagem('Sinal de VENDA: Cruzamento de MA de baixo para cima')

# Rodar o bot do Telegram
updater = Updater(token=bot_token, use_context=True)
dispatcher = updater.dispatcher

updater.start_polling()

# Encerrar o bot
updater.idle()
