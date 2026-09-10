# Twilio SMS Booking System

An SMS-based appointment booking prototype built with Node.js, Express, and Twilio. Users can reply to a Twilio SMS webhook to choose a service, weekday, and appointment time.

![Twilio SMS](images/twilio-sms.png)

## Features

- Handles incoming Twilio SMS messages through a webhook.
- Guides users through a booking conversation.
- Supports gym visits, personal trainers, and massages.
- Collects a weekday and appointment time.
- Stores the conversation state in an Express session.
- Returns TwiML responses to Twilio.

## Tech Stack

- Node.js
- Express
- Twilio
- Express Session
- dotenv

## Project Structure

```text
.
├── backend/
│   ├── .gitignore
│   ├── package.json
│   ├── yarn.lock
│   └── src/
│       ├── bookingHelper.js
│       └── main.js
└── images/
    └── twilio-sms.png
```

## Requirements

- Node.js 12 or later
- Yarn or npm
- A Twilio account and phone number capable of sending SMS
- A public HTTPS URL for the Twilio webhook in development or production

## Installation

```bash
cd backend
yarn install
```

Create a `backend/.env` file:

```env
ACCOUNT_SID=your_twilio_account_sid
TOKEN_SID=your_twilio_api_key_sid
TOKEN_SECRET=your_twilio_api_key_secret
PHONE_NUMBER=your_twilio_phone_number
MY_NUMBER=your_destination_phone_number
SESSION_SECRET=replace_with_a_long_random_value
EXPRESS_PORT=3001
WEEKDAYS=monday,tuesday,wednesday,thursday,friday
```

The `.env` file is ignored by Git and must not be committed.

## Running the Server

```bash
cd backend
yarn start
```

The server listens on port `3001` by default. Set `EXPRESS_PORT` to use another port.

## Endpoints

### Health Check

```text
GET /test
```

Returns a simple text response confirming that the server is running.

### Incoming SMS Webhook

```text
POST /receive-sms
```

Configure this URL as the incoming message webhook for the Twilio phone number. Twilio should send form-encoded requests containing the `Body` field.

The conversation follows this flow:

1. The user selects a service.
2. The user selects a weekday.
3. The user selects an appointment time.
4. The system returns a booking confirmation.

For local development, expose the server with a tunneling tool such as ngrok and use the generated HTTPS URL as the Twilio webhook URL.

## Notes

- Booking state is kept in the Express session and is not persisted to a database.
- The available weekdays are configured through `WEEKDAYS`.
- Twilio credentials and phone numbers must be supplied through environment variables.

## License

This project is licensed under the MIT License.
