# Description

Download emails from Gmail.
Query gmail e-mail for a specified date range. Output is saved by email thread
within the folder provided. You can also specify [search
rules](https://support.google.com/mail/answer/7190?hl=en).

## Setup

```
pip install git+https://github.com/kylebarron/gmail_download
```

You also need to get a key from Gmail to allow it to receive queries from Python.
Adapted from the [Gmail API quickstart](https://developers.google.com/gmail/api/quickstart/python):

1. Use [this wizard](https://console.developers.google.com/start/api?id=gmail) to create or select a project in the Google Developers Console and automatically turn on the API. Click **Continue**, then **Go to credentials**.
2. On the **Add credentials to your project** page, click the **Cancel** button.
3. At the top of the page, select the **OAuth consent screen** tab. Select an **Email address**, enter a **Product name** if not already set, and click the **Save** button.
4. Select the **Credentials** tab, click the **Create credentials** button and select **OAuth client ID**.
5. Select the application type **Other**, enter the name "Gmail API Quickstart", and click the **Create** button.
6. Click **OK** to dismiss the resulting dialog.
7. Click the `file_download` (Download JSON) button to the right of the client ID.

You'll need to use that file location for the `client_secret_path` argument of `gmail_query()`.

## Usage

```python
from gmail_query import gmail_query
q = gmail_query(
  email_address='janedoe@example.com',
  outdir='/path/to/output',
  client_secret_path='~/.config/gmail-download/client_secret.json',
  credential_path='~/.credentials/gmail_download.json'):
q.query(
  begin_date='2018-01-01',
  end_date='today',
  label=None,
  g_query='from:johndoe@example.com subject:dinner',
  tz_locale='America/New_York')
```

## Documentation

### `gmail_query`

This is the class that sets up a connection with Google's servers. Arguments are:

- `email_address` (`str`): your email address
- `outdir` (`str`): the folder in which to save emails
- `client_secret_path` (`str`): the path to the `client_secret.json` file you downloaded in step 7 of the setup
- `credential_path` (`str`): the path to save the OAuth2 credentials that are generated the first time you use the program

### `gmail_query.query`

This is the primary function of the `gmail_query` class. It downloads emails for a given query.

- `begin_date` (`str`): Date (formatted `YYYY-MM-DD`) to begin searching for emails
- `end_date` (`str`): Date (formatted `YYYY-MM-DD`) to end searching for emails (inclusive)
- `label` (`str`): label to download messages for
- `g_query` (`str`): [Google search string](https://support.google.com/mail/answer/7190?hl=en)


## To Do

- [ ] Download attachments.
- [ ] Improve documentation.
- [ ] Verbose option
