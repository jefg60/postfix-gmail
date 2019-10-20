Role Name
=========

Configures postfix on linux hosts to forward emails via a gmail account.

Requirements
------------

You need a gmail account. You might need to create an app password for postfix to use with your gmail account, as per https://support.google.com/accounts/answer/185833?hl=en (you definitely will if using 2 factor auth).

Role Variables
--------------

Defaults

```
postfix_config_file: "/etc/postfix/main.cf"
postfix_aliases_file: "/etc/aliases"
postfix_relay_passwords_file: "/etc/postfix/relay_passwords"
postfix_relayhost: "[smtp.gmail.com]:587"

postfix_relay_password: "{{ lookup('env','GMAILPOSTFIX') }}"
postfix_relay_user: "test@example.com"
postfix_ca_certs: "/etc/ssl/certs/ca-certificates.crt"

postfixaliases: (dict)
(from geerlingguy.postfix dependency role)
postfix_inet_interfaces: (IP)

e.g:
postfixaliases:
  root:
    addressalias: "test"
  test:
    addressalias: "test@example.com"
postfix_inet_interfaces: 127.0.0.1
```

You will want to override the relay password and relay user vars to match the google account used for sending emails. I suggest you put postfix_relay_password in a vault or set the env var GMAILPOSTFIX instead of just saving it in a plaintext vars file, of course.

Dependencies
------------

- geerlingguy.postfix

License
-------

GPLv3

Author Information
------------------

jeff@jeffhibberd.com
