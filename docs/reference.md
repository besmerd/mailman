# Reference

## Mails
The `mails` section defines the messages which should be generated. The
following configuration would create a message from 'sender@example.com' to
'recipient@example.com'

```yaml
---
mails:
  - sender: sender@example.com
    recipients: recipient@example.com
    subject: Hello World
    text_body: This is a simple hello.
```

name
: An optional reference name for the message

description
: An optional description for the message

sender
: Defines the envelope sender

recipients
: Defines a single or a list of recipients

subject
: Subject of the message

text_body
: A MIME part of type `text/plain`

text_html
: A MIME part of type `text/html`

from
: Message from, defaults to `sender`

to
: Message to, defaults to `recipients`

loop:
: List of parameters to loop over.

## Vars
The `vars` section holds variables which can be used in other sections
like `mails` or `defaults`.

```yaml
---
vars:
  names:
    - Alice
    - Bob
    - Rachel

mails:
  - sender: sender@example.com
    recipients: recipient@example.com
    subject: 'Hello {{ item }}'
    text_body: This is a simple hello.
    loop: '{{ names }}'
```

## Defaults
The `defaults` section can be used for properties that should apply for all
messages in a given configuration file. Properties defined in the `mails`
section have a higher precedence and therefore overwrite the default values.

The following configuration would result in a message from *sender@example.com*
to *recipient@example.net*
```yaml
---
defaults:
  sender: sender@example.com
  recipients: recipient@example.com

mails:
  - subject: Hello World
    text_body: This is a simple hello.

  - sender: other@example.com
    subject: Hello World
    text_body: This is a simple hello.
```