# Create or Update Project Card

A GitHub action to remove project card.

## Usage

### Create a project card

```yml
      - name: Remove a Specific Project Card
        uses: aj-stein-nist/remove-project-card@v0.0.1
        with:
          project-name: My project
          issue-number: 1
```

### Create a card in an organization or user project

When creating cards in an organization or user project, a `repo` and `admin:org` scoped [Personal Access Token (PAT)](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) is required.

```yml
      - name: Remove a Specific Card in a Project in an
        uses: aj-stein-nist/remove-project-card@v0.0.1
        with:
          token: ${{ secrets.PAT }}
          project-location: my-org
          project-name: My project
          issue-number: 1
```

### Remove a card for all closed issues

```yml
on:
  issues:
    types: [closed]
jobs:
  createCard:
    runs-on: ubuntu-latest
    steps:
      - name: Create or Update Project Card
        uses: aj-stein-nist/remove-project-card@v0.0.1
        with:
          project-name: My project
```

### Action inputs

| Name | Description | Default |
| --- | --- | --- |
| `token` | `GITHUB_TOKEN` or a `repo` scoped [PAT](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token). | `GITHUB_TOKEN` |
| `project-location` | The location of the project. Either a repository, organization, or user. | `github.repository` (current repository) |
| `project-number` | (**semi-required**) The number of the project. Either `project-number` OR `project-name` must be supplied. | |
| `project-name` | (**semi-required**) The name of the project. Either `project-number` OR `project-name` must be supplied. Note that a project's name is not unique. The action will use the first matching project found. | |
| `repository` | The GitHub repository containing the issue or pull request. | `github.repository` (current repository) |
| `issue-number` | The issue or pull request number to associate with the card. | `github.event.issue.number` |

### Action outputs

The action outputs `card-id` for use in later workflow steps.

```yml
      - name: Create or Update Project Card
        id: coupc
        uses: aj-stein-nist/remove-project-card@v0.0.1
        with:
          project-name: My project
          issue-number: 1
      - name: Check output of card removed
        run: echo ${{ steps.coupc.outputs.card-id }}
```

## License

[MIT](LICENSE)
