# Telegrambot-using-AWS
Building a Telegram Bot with AWS Lambda and API Gateway.
![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/e6de43ed-cc93-4f2d-8ad1-950b96bd4402)

# Create a Telegram Bot using BOTFATHER
![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/89b6dec2-072b-48e5-862a-594c9ba07525)

# Create a Lambda Function

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/1632cd8c-d407-4002-89cb-707af9045d3a)

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/8e626710-412b-47f1-b586-e1d37e1da2ae)

# create HTTP API 

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/dc4f6f65-e380-45af-9289-2cde9d55bcb8)

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/83661fb9-6e58-4874-9236-261032c192d2)

Copy the URL.
# Create a Post Method in POSTMAN 

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/f691daaa-7426-44d9-85ea-dac772071afe)

# write the python code in Lambda to connect with clean URL

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/54190e2a-c576-481c-93e0-a5963f16e3ee)

# Code 
import json
import requests

def lambda_handler(event, context):
    try:
        print("Received event:", json.dumps(event))

        if 'body' not in event:
            return {
                "statusCode": 400,
                "body": json.dumps("Invalid request format")
            }

        body = json.loads(event['body'])
        print("Received body:", json.dumps(body))

        message = body.get('message')
        
        if message is None or 'text' not in message:
            return {
                "statusCode": 400,
                "body": json.dumps("Invalid message format")
            }

        message_text = message['text']
        print("Message text:", message_text)

        # Shorten the URL using CleanURI or another service
        shortened_url = shorten_url(message_text)
        print("Shortened URL:", shortened_url)

        chat_id = message['chat']['id']

        # Send the shortened URL back to the user
        send_telegram_message(chat_id, shortened_url)

        return {
            "statusCode": 200,
            "body": json.dumps("URL shortened successfully")
        }
    except Exception as e:
        print("Error:", str(e))
        return {
            "statusCode": 500,
            "body": json.dumps("Internal server error")
        }

def shorten_url(url):
    # Implement URL shortening logic here, e.g., using CleanURI or a custom service
    data = {'url': url}
    response = requests.post('https://cleanuri.com/api/v1/shorten', data=data)
    return response.json()['result_url']

def send_telegram_message(chat_id, text):
    # Implement sending a message to Telegram here
    bot_token = 'YOUR_BOT_TOKEN'
    url = f'https://api.telegram.org/bot{bot_token}/sendMessage'
    payload = {
        'chat_id': chat_id,
        'text': text
    }
    r = requests.post(url, json=payload)

# Now go to the telegram and give a URL

![image](https://github.com/chaudharyvishalrawat/Telegrambot-using-AWS/assets/104204831/c5227b99-bccb-49de-9afc-8c7d3f6e0162)

# Thank you for reading 😊😊

