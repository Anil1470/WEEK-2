# WEEK-2
This is about 50 percent of my work and it shows that how to develop it and how to send a notification to them for alertness, thank you .
def send_sms_alert(message):
    client = Client(TWILIO_SID, TWILIO_AUTH)
    client.messages.create(body=message, from_=TWILIO_NUMBER, to=MY_NUMBER)

def fetch_weather():
    url = f"http://api.openweathermap.org/data/2.5/forecast?q={CITY},{COUNTRY}&appid={OPENWEATHER_KEY}&units={UNITS}"
    return requests.get(url).json()

def compute_risk(avg_temp, avg_humidity, total_precip):
    temp_contrib = max(0, min(1, (avg_temp - 30) / 15))
    humidity_contrib = max(0, min(1, (50 - avg_humidity) / 50))
    precip_contrib = max(0, min(1, (20 - total_precip) / 20))
    score = (0.4 * temp_contrib) + (0.3 * humidity_contrib) + (0.3 * precip_contrib)

    if score < 0.4: return "LOW", score
    elif score < 0.7: return "MEDIUM", score
    else: return "HIGH", score
