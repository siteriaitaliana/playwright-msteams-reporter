# Microsoft Teams reporter for Playwright

This is a Microsoft Teams reporter for Playwright. It allows you to send the test results to a Microsoft Teams channel and mention users on failure.

## Prerequisites

To make use of this reporter, you need to create a incoming webhook for your Microsoft Teams channel. You can find more information on how to do this in the [Microsoft documentation](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook?tabs=newteams%2Cdotnet#create-an-incoming-webhook).

> **Info**: You need to copy the `webhook URL` from the configuration as you will need it to configure the reporter.

Here you can see an example card for successful test results:

![Microsoft Teams card for successful test results](./assets/success.png)

And here you can see an example card for failed test results:

![Microsoft Teams card for failed test results](./assets/failure.png)

## Installation

Install from npm:

```bash
npm install playwright-msteams-reporter
```

## Usage

You can configure the reporter by adding it to the `playwright.config.js` file:

```javascript
import { defineConfig } from '@playwright/test';

export default defineConfig({
  reporter: [
    ['list'],
    [
      'playwright-msteams-reporter',
      {
        webhookUrl: "<webhookUrl>",
      }
    ]
  ],
});
```

> More information on how to use reporters can be found in the [Playwright documentation](https://playwright.dev/docs/test-reporters).

## Configuration

The reporter supports the following configuration options:

| Option | Description | Type | Required | Default |
| --- | --- | --- | --- | --- |
| `webhookUrl` | The Microsoft Teams webhook URL | `boolean` | `true` | `undefined` |
| `title` | The notification title | `string` | `false` | `Playwright Test Results` |
| `linkToResultsUrl` | Link to the test results | `string` | `false` | `undefined` |
| `linkToResultsText` | Text for the link to the test results | `string` | `false` | `View test results` |
| `notifyOnSuccess` | Notify on success | `boolean` | `false` | `true` |
| `mentionOnFailure` | Mention users on failure (comma separated list) | `string` | `false` | `undefined` |
| `mentionOnFailureText` | Text to mention users on failure | `string` | `false` | `{mentions} please validate the test results.` |
| `quiet` | Do not show any output in the console | `boolean` | `false` | `false` |
| `debug` | Show debug information | `boolean` | `false` | `false` |

### Mention users

With the `mentionOnFailure` option, you can mention users in the Microsoft Teams channel when a test fails. You can provide an array of users to mention.

The format can be either the full name and email (`"Full name <email>"`) or just the email address (`email`). The reporter will replace the `{mentions}` placeholder in the `mentionOnFailureText` with the mentioned users.

```javascript
{
  mentionOnFailure: "Elio Struyf <mail@elio.dev>,mail@elio.dev",
  mentionOnFailureText: "{mentions} check those failed tests!"
}
```

### Link to the results

With the `linkToResultsUrl` option, you can provide a link to the test results. You can for instance use this to view the test results on your CI/CD platform.

```javascript
{
  // The link to your GitHub Actions workflow run
  linkToResultsUrl: `${process.env.GITHUB_SERVER_URL}/${process.env.GITHUB_REPOSITORY}/actions/runs/${process.env.GITHUB_RUN_ID}`,
}
```

<br />

[![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Festruyf%2Fplaywright-msteams-reporter&countColor=%23263759)](https://visitorbadge.io/status?path=https%3A%2F%2Fgithub.com%2Festruyf%2Fplaywright-msteams-reporter)
