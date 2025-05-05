from flask import Flask, request
from twilio.twiml.messaging_response import MessagingResponse

app = Flask(__name__)

@app.route("/whatsapp", methods=["POST"])
def whatsapp_reply():
    incoming_msg = request.values.get("Body", "").lower()
    resp = MessagingResponse()
    msg = resp.message()

    if "hola" in incoming_msg:
        msg.body("¡Hola! Soy tu bot de WhatsApp 🤖")
    elif "adiós" in incoming_msg:
        msg.body("¡Hasta luego! 👋")
    else:
        msg.body("No entendí eso. Escribe 'hola' o 'adiós'.")
    
    return str(resp)
