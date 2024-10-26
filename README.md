<h1 align="center" id="title">Activity Log</h1>

![activity log](https://socialify.git.ci/TheDanniCraft/activity-log/image?forks=1&issues=1&language=1&logo=https%3A%2F%2Favatars.githubusercontent.com%2Fu%2F66677362&name=1&owner=1&pattern=Solid&pulls=1&stargazers=1&theme=Auto)

<p align="center">
    <img src="https://img.shields.io/badge/Made%20with%20Love%E2%9D%A4%EF%B8%8F-black?style=for-the-badge" alt="made with love">
    <img src="https://img.shields.io/badge/Node.JS-node?style=for-the-badge&amp;logo=nodedotjs&amp;logoColor=white&amp;color=%235FA04E" alt="typescript">
</p>

A GitHub Action that automatically updates your README file with the latest activity from your GitHub account. Customize the displayed events, set a limit on the number of events, and ignore specific event types. Ideal for keeping your personal README file current with recent contributions and changes.

## 🛠️Features

- Customizable Event Limits
- Event Filtering
- Flexibility with Inputs

## ✍️ EXAMPLE EXAMPLE

<!--START_SECTION:activity-->
1. undefined
2. 🆕 Opened an issue [#7](https://github.com/huntertoby/UnityFpsPractice/issues/7) in [huntertoby/UnityFpsPractice](https://github.com/huntertoby/UnityFpsPractice)
3. undefined
4. 🎉 Created a new repository [huntertoby/TestProject](https://github.com/huntertoby/TestProject)
5. ➕ Created a new branch [`main`](https://github.com/huntertoby/TestProject/tree/main) in [huntertoby/TestProject](https://github.com/huntertoby/TestProject)
6. ❌ Closed an issue [#6](https://github.com/huntertoby/UnityFpsPractice/issues/6) in [huntertoby/UnityFpsPractice](https://github.com/huntertoby/UnityFpsPractice)
7. 🆕 Opened an issue [#6](https://github.com/huntertoby/UnityFpsPractice/issues/6) in [huntertoby/UnityFpsPractice](https://github.com/huntertoby/UnityFpsPractice)
8. ❌ Closed an issue [#5](https://github.com/huntertoby/UnityFpsPractice/issues/5) in [huntertoby/UnityFpsPractice](https://github.com/huntertoby/UnityFpsPractice)
9. 📝 Committed to [huntertoby/activity-log](https://github.com/huntertoby/activity-log/commit/a3ae79ba0430ec6f8329fdca77e484bdf5e4de7f)
10. 📝 Committed to [huntertoby/activity-log](https://github.com/huntertoby/activity-log/commit/e6c8facc7cedb819de1a99ff87a4868e9c8fb1cb)
<!--END_SECTION:activity-->

## 📖Usage

### 1. Add Sections to `README.md`

Include the following placeholders in your `README.md` where you want the activity log to appear:

```markdown
<!--START_SECTION:activity-->
<!--END_SECTION:activity-->
```

For a reference example, you can view this [sample `README.md`](https://github.com/TheDanniCraft/activity-log/blob/master/README.md?plain=1#L20-L31).

### 2. Create a Personal Access Token

<details open>
  <summary><strong>Quick Setup</strong> <i>(Recommended)</i></summary>

  1. To create a personal access token with the necessary permissions, click this [link to create a new token](https://github.com/settings/tokens/new?description=Github%20Activity%20Log%20(TheDanniCraft/activity-log)&scopes=repo). This link pre-fills the token description and scopes for your convenience.
  2. On the token creation page, review the pre-filled data and set the expiration date to "Never".
  3. Click "Generate token" and copy the token (be sure to save it as you won’t be able to see it again).

</details>

<details>
  <summary><strong>Manual Setup</strong></summary>

  1. Go to your GitHub [Personal Access Tokens settings](https://github.com/settings/tokens).
  2. Click on "Generate new token".
  3. Provide a descriptive name for the token, such as `Github Activity Log (TheDanniCraft/activity-log)`.
  4. Select the `repo` scope (recommended if you want private repo activity to show up).
  5. Set the expiration date to "Never".
  6. Click "Generate token" and copy the token (be sure to save it as you won’t be able to see it again).

</details>

### 3. Add the Token as a Repository Secret

1. Navigate to your GitHub repository.
2. Go to "Settings" > "Secrets and variables" > "Actions".
3. Click "New repository secret".
4. Name the secret (e.g., `TOKEN`).
5. Paste the personal access token into the value field.
6. Click "Add secret".

### 4. Create the Workflow File

Create a new file in your repository under `.github/workflows/`, for example, `activity-log.yml`. Add the following content to this file:

```yml
# .github/workflows/update-activity.yml:

name: Update GitHub Activity

on:
  schedule:
    - cron: "*/30 * * * *" # Runs every 30 minutes
  workflow_dispatch: # Allows manual triggering

jobs:
  update-activity:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Update GitHub Activity
        uses: TheDanniCraft/activity-log@v1
        with:
          GITHUB_USERNAME: "thedannicraft"
          GITHUB_TOKEN: ${{ secrets.TOKEN }} # Ensure this matches the secret name in repository settings
```

Take a look at all possible [Inputs](#inputs) for customization

The above job runs every half an hour, you can change it as you wish based on the [cron syntax](https://crontab.guru).

Please note that only those public events that belong to the following list show up:

- `CreateEvent`
- `PushEvent`
- `IssuesEvent`
  - `opened`
  - `edited`
  - `closed`
  - `reopened`
  - `assigned`
  - `unassigned`
  - `labeled`
  - `unlabeled`
- `PullRequestEvent`
  - `opened`
  - `edited`
  - `closed`
  - `merged`
  - `reopened`
  - `assigned`
  - `unassigned`
  - `review_requested`
  - `review_request_removed`
  - `labeled`
  - `unlabeled`
  - `synchronize`
- `ReleaseEvent`
- `ForkEvent`
- `CommitCommentEvent`
- `IssueCommentEvent`
- `PullRequestReviewEvent`
- `PullRequestReviewCommentEvent`
- `RepositoryEvent`
- `WatchEvent`
- `StarEvent`
- `PublicEvent`
- `GollumEvent`

You can find an example [here](https://github.com/TheDanniCraft/activity-log/blob/master/.github/workflows/update-activity.yml).

### Inputs

| **Input**         | **Description**                                                                                                                                                                 | **Required**     | **Default**                             | **Possible Options**                                                        |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------------------------------------|-----------------------------------------------------------------------------|
| `GITHUB_USERNAME` | Your GitHub username.                                                                                                                                                           | ✅               | `-`                                     | A valid GitHub username                                                    |
| `GITHUB_TOKEN`    | Your GitHub token.                                                                                                                                                              | ✅               | `-`                                     | A valid GitHub access token (must belong to the specified GitHub username) |
| `EVENT_LIMIT`     | The maximum number of events to display.                                                                                                                                        | ❌               | `10`                                    | Any positive integer                                                       |
| `OUTPUT_STYLE`    | Specifies the format in which your output should be rendered. <br> <ins>Must be one of:</ins> <br> - `MARKDOWN`: Output in Markdown format <br> - `HTML`: Output in HTML format | ❌               | `MARKDOWN`                              | `MARKDOWN` or `HTML`                                                       |
| `IGNORE_EVENTS`   | The events to ignore, specified as a JSON array.                                                                                                                                | ❌               | `[]`                                    | JSON array of event types (e.g., `["PushEvent", "PullRequestEvent"]`)               |
| `README_PATH`     | The path to your README file.                                                                                                                                                   | ❌               | `README.md`                             | Any valid file path                                                        |
| `COMMIT_MESSAGE`  | Your commit message.                                                                                                                                                            | ❌               | `-`                                     | Any valid commit message                                                   |

## 📜License

[MIT](https://choosealicense.com/licenses/mit/)

## ✍️Authors

- [@thedannicraft](https://www.github.com/thedannicraft)
