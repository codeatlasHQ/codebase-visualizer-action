# Codeatlas codebase-visualizer-action

> Codeatlas visualizes codebases.

--> TODO: Add picture of the dashboard

The codebase-visualizer-action creates a visualization of your codebase and makes it available at `https://codeatlas.dev/github/<REPO_OWNER>/<REPO_NAME>/<?COMMIT_OR_BRANCH>`. 

Explore sample visualizations of well-known open-source projects in our [gallery](codeatlas.dev/gallery)!

## Usage
In order to use this action, `Settings - Actions - General - Allow GitHub Actions to create and approve pull requests` needs to be activated! If your repo is part of a GitHub organisation, you need to enable this setting in the organisation settings first.

To add Codeatlas into an existing Actions pipeline, add this repository as a step within your workflow.yml file like this:

```
steps:
  - uses: actions/checkout@v3
  - uses: codeatlasHQ/codebase-visualizer-action@v1-beta
  	with:
  	  sub_directory: src/example/  # optional
```

The action will then run the main Codeatlas Docker image (maintained in the [codebase-tessellator](https://github.com/codeatlasHQ/codebase-tessellator) project) to create a snapshot of the repo.

Upon a successful run, `codeatlas-bot` will create a branch named `codeatlas-preview` and add the data necessary for the visualization to the `.codeatlas` directory. It will then raise a PR to add this visualization snapshot to your default branch. The bot will keep updating and overwriting the same PR everytime the action runs. After merging this PR, the interactive visualization will become available at `https://codeatlas.dev/github/<REPO_OWNER>/<REPO_NAME>/<?COMMIT_OR_BRANCH>`.

How often to trigger: 
We've found it overkill to visualize the project with every push-event, so we recommend using:
1) the `on: [tag]` workflow trigger to update the visualization on each release or
2) the `on: [workflow_dispatch]` trigger to run the action manually and update the visualization whenever you want.

See [this repo](https://github.com/codeatlasHQ/codebase-tessellator) for a working setup.

## Private Repositories
This action does not yet support private repositories! The action should run through, but you will not be able to access your visualizations through codeatlas.dev.

## Arguments

| Input | Description | Default |
| :---:     |     :---:   |    :---:   |
| `sub_directory` | (Optional) Specify the root directory of your codebase. No leading slash allowed. | "" |

## Roadmap
Check out our roadmap on Trello: https://trello.com/b/jg1kn5c2/codeatlas-roadmap

