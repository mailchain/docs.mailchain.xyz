# Command Line Errors

The table below give common reasons for error found in the output of the mailchain command line application:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Error</th>
      <th style="text-align:left">Likely Cause</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ERRO[ {date} ] status 500: secretbox: Could not decrypt invalid input</td>
      <td
      style="text-align:left">Message has been retrieved but could not be decrypted. Ensure you entered
        the right passphrase for your keystore.</td>
    </tr>
    <tr>
      <td style="text-align:left">ERRO[ {date} ] status 500: insufficient funds for gas * price + value</td>
      <td
      style="text-align:left">The balance on this address is insufficient to send a message. If you
        have a balance, check you are sending on the correct network.</td>
    </tr>
    <tr>
      <td style="text-align:left">ERRO[ {date} ] status 500: No transactions found for <code>address</code>
      </td>
      <td style="text-align:left">
        <p>The recipient address has not yet sent a transaction on this network.
          This means the public key associated with the address is not available
          to encrypt the message.</p>
        <p>To resolve this, the recipient address needs to have sent at least one
          transaction (even zero value).</p>
      </td>
    </tr>
  </tbody>
</table>

