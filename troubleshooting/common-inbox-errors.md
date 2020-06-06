# Common Inbox Errors

<table>
  <thead>
    <tr>
      <th style="text-align:left">Error</th>
      <th style="text-align:left">Fix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&quot;Mailchain client does not seem to be running&quot;</td>
      <td style="text-align:left">
        <ol>
          <li>Check you have <a href="../getting-started.md">downloaded and configured</a> the
            Mailchain client.</li>
          <li>Check your <a href="../mailchain-web-inbox/configuring-the-web-interface.md#changing-the-server-settings">server settings</a> are
            correct.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&quot;Your Mailchain client version is A.B.C. Please upgrade it to version
        X.Y.Z to ensure things work as expected.&quot;</td>
      <td style="text-align:left">
        <p>See <a href="../upgrading.md">Upgrading Mailchain</a> for further information
          on how to upgrade.</p>
        <p></p>
        <p>NOTE: To check the latest release version, visit <a href="https://github.com/mailchain/mailchain/releases">Mailchain releases on Github</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&quot;Error 500: could not send message: could not send transaction: Insufficient
        funds. The account you tried to send transaction from does not have enough
        funds. Required 46528000000000 and got: 0.&quot;</td>
      <td style="text-align:left">
        <p>The address you are sending FROM does not have enough balance to pay the
          gas cost to send a transaction.</p>
        <p></p>
        <p>Check that you are sending on the right network and that you have a balance
          on that account.</p>
      </td>
    </tr>
  </tbody>
</table>



