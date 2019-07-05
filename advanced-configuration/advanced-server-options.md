# Advanced Serve Options

The mailchain application runs with the default settings using the following command:

```bash
mailchain serve
```

To configure advanced options, run:

```bash
mailchain serve [flags]
```

| Flag | Options |
| :--- | :--- |
| --cors-allowed-origins _string_  | Allowed origins for CORS \(default "\*"\) |
| --cors-disabled | Disable CORS on the server \(enabled by default\) |
| --passphrase _string_ | Passphrase to decrypt key for sending / receiving messages. If this is not entered, the application with prompt you to enter the passphrase. |
| --port _int_ | Port to run server on \(default 8080\) |

Global Flags

| Flag | Options |
| :--- | :--- |
| --config _string_ | The location of the config file \(default is $HOME/.mailchain/.mailchain.yaml\) |
| --empty-passphrase | No passphrase and no prompt |
| --log-level _string_  | Set the log level \[Panic,Fatal,Error,Warn,Info,Debug\] \(default "warn"\) |

For more information, run:

```bash
mailchain serve --help
```



