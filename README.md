# Notification Action

This GitHub Action sends a notification to Discord with a given status. It provides an easy way to notify your team about the current status of your project's build.

![preview](/images/preview.png)

## Inputs

| Name      | Description                                          | Required          | Default  |
|-----------|------------------------------------------------------|-------------------|----------|
| status    | The build status (e.g., Start, Done, Error)          | Yes               | *        |
| webhook   | The Discord webhook                                  | Yes               | *        |
| icon      | The emoji icon for the status                        | No                | 👨🏼‍💻       |
| title     | The title of your app                                | No                | ${{ github.repository }}      |

## Outputs

| Name         | Description                                      |
|--------------|--------------------------------------------------|
| version      | The release version of the app (e.g., get it from release/1.0.7) |
| build_number | The incremented run number                       |

## Usage

To use this action in your workflow, add the following step:

```yaml
- name: Discord notification
  id: discord
  uses: emvakar/discord-notification-action@v1.0.5
  with:
    status: 'Done'
    icon: '✅'
    title: 'My App'
    webhook: ${{ secrets.WEBHOOK }}
```

## Example with minimum variables

Here's an example of how to use this action in a workflow with minimum variables:

```yml
jobs:
  some_job:
    # ...

  notification_done:
    name: Discord notification on success()
    if: ${{ success() }}
    needs: [some_job]
    runs-on: ubuntu-latest
    steps:
      - name: Discord notification
        id: discord
        uses: emvakar/discord-notification-action@v1.0.5
        with:
          status: 'Done'
          webhook: ${{ secrets.DISCORD_WEBHOOK }}

```