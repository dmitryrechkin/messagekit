# MessageHub SendGrid

**MessageHub SendGrid is a TypeScript library that provides integration with the SendGrid email service, allowing for seamless email sending capabilities within your applications.** This package extends the core functionality of MessageHub to support SendGrid as an email provider.

## Installation

Install the package using pnpm:

```bash
pnpm add @messagehub/sendgrid
```

## Features

- **Email Sending**: Easily send emails using the SendGrid API.
- **Attachment Support**: Send emails with attachments.
- **Requires Core Package**: This package requires the `@messagehub/core` package for functionality.

## Usage

### Sending an Email

The `sendEmail` function can be used as follows:

```typescript
import { sendEmail } from '@messagehub/core';

const emailMessage = {
  from: [{ email: 'sender@example.com', name: 'Sender Name' }],
  to: [{ email: 'recipient@example.com', name: 'Recipient Name' }],
  subject: 'Hello from MessageHub SendGrid',
  text: 'This is a test email sent using MessageHub with SendGrid.',
  html: '<p>This is a test email sent using MessageHub with SendGrid.</p>',
  attachments: [
    {
      content: 'base64-encoded-content',
      filename: 'attachment.txt',
      path: '/path/to/attachment.txt',
    },
  ],
};

const config = {
  MESSAGE_PROVIDER: 'sendgrid',
  SENDGRID_API_KEY: process.env.SENDGRID_API_KEY,
  SENDGRID_API_URL: process.env.SENDGRID_API_URL, // Optional
};

sendEmail(emailMessage, config)
  .then(response => {
    if (response.success) {
      console.log('Email sent successfully:', response.data);
    } else {
      console.error('Error sending email:', response.messages);
    }
  })
  .catch(error => {
    console.error('Error sending email:', error);
  });
```

### Configuration

Configuration for the `sendEmail` function can be defined in a `.env` file. The naming convention for the configuration variables is as follows:

- `MESSAGE_PROVIDER`: The name of the provider to use.
- `SENDGRID_API_KEY`: The API key for authenticating with the SendGrid API.
- `SENDGRID_API_URL`: An optional custom API URL.

Example `.env` file:

```
SENDGRID_API_KEY=your_sendgrid_api_key
SENDGRID_API_URL=https://api.sendgrid.com
```

### Extensibility

The `@messagehub/sendgrid` package is an implementation of the SendGrid email provider. The core functionality is provided by the `@messagehub/core` package, which is designed to be extensible. You can create new email providers by implementing the `EmailProviderFactoryInterface` and `EmailSenderInterface` in the core package. This allows you to add support for additional email services in the future.

## Rationale

The `@messagehub/sendgrid` package is designed to provide integration with the SendGrid API for managing email sending workflows in TypeScript applications. By using the core package, developers can easily integrate SendGrid capabilities into their domain-driven designs and AI-driven processes.

## Contributing

Contributions are welcome! Feel free to fork this project and submit pull requests. Before submitting, please ensure your code passes all linting and unit tests.

You can format code using:

```bash
pnpm format
```

You can run unit tests using:

```bash
pnpm test