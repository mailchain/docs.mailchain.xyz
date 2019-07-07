# Command Line Errors

The table below give common reasons for error found in the output of the mailchain command line application:

| Error | Likely Cause |
| :--- | :--- |
| ERRO\[ {date} \] status 500: secretbox: Could not decrypt invalid input | Message has been retrieved but could not be decrypted. Ensure you entered the right passphrase for your keystore. |
| ERRO\[ {date} \] status 500: insufficient funds for gas \* price + value | The balance on this address is insufficient to send a message. If you have a balance, check you are sending on the correct network. |



