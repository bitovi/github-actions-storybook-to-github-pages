# Deploy Storybook to GitHub Pages 

`bitovi/github-actions-storybook-to-github-pages` builds and deploys a Storybook application to GitHub Pages.

This action uses the new GitHub Actions publishing method which allows you to create an artifact that contains the result of the build and serves the files in the artifact on the Pages site. There’s no need to check files back into your repository, keeping it nice and clean.


## You are here
This action deploys Storybook to Github Pages.  The build process should create static files and put them into a build direcory that will be moved into your Pages hosting location.  

If you would like to deploy a backend app/service, check out our other actions:
| Action | Purpose |
| ------ | ------- |
| [Deploy Docker to EC2](https://github.com/bitovi/github-actions-deploy-docker-to-ec2) | Deploys a repo with a Dockerized application to a virtual machine (EC2) on AWS |
| [Deploy static site to AWS (S3/CDN/R53)](https://github.com/marketplace/actions/deploy-static-site-to-aws-s3-cdn-r53) | Hosts a static site in AWS S3 with CloudFront |

# Need help or have questions?
This project is supported by [Bitovi, A DevOps consultancy](https://www.bitovi.com/services/devops-consulting).

You can **get help or ask questions** on our:

- [Discord Community](https://discord.gg/J7ejFsZnJ4Z)


Or, you can hire us for training, consulting, or development. [Set up a free consultation](https://www.bitovi.com/services/devops-consulting).

# Basic Use

> **Note: ** Be sure to [set up your project for actions deployed pages](#set-up-your-project-for-actions-deployed-pages).

For basic usage, create `.github/workflows/deploy.yaml` with the following to build on push.
```yaml
on:
  push:
    branches:
      - "main" # change to the branch you wish to deploy from

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - id: build-publish
      uses: bitovi/github-actions-storybook-to-github-pages@v1.0.0
      with:
        path: build # change to your build folder
```

## Set up your project for Actions deployed Pages
- In the project repo in GitHub, go to Settings > Pages.
- For the source, select GitHub Actions
- No further configuration is needed.  

![For the source, select GitHub Actions](./assets/github%20action%201.webp)

> **Note:** Your Repository must be set to public for GitHub Pages to serve content.

# Inputs

The following inputs can be used as `step.with` keys

| Name             | Type    | Description                        |
|------------------|---------|------------------------------------|
| `checkout`          | T/F  | Set to `false` if the code is already checked out (Default is `true`) (Optional) |
| `path` | String | Path of output files, Default is `dist/storybook` (Optional)|
| `build_command` | String | Specifies the command to run after `npm ci` for the build, Default is `npm run build` (Optional)|

# Customizing

## Repository Environments
To surface published url to the root of the repo via a GitHub Environment, add the following to your workflow:
```yaml
# ...etc
jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.build-publish.outputs.page_url }}
    # ...etc
```

> *Note:* This is helpful when you have a custom domain

<details>
  <summary>Full example with environment</summary>

  ```yaml
  on:
    push:
      branches:
        - "main" # change to the branch you wish to deploy from

  permissions:
    contents: read
    pages: write
    id-token: write

  jobs:
    deploy:
      environment:
        name: github-pages
        url: ${{ steps.build-publish.outputs.page_url }}
      runs-on: ubuntu-latest
      steps:
      - id: build-publish
        uses: bitovi/github-actions-storybook-to-github-pages@v1.2.0
        with:
          path: build # change to your build folder
  ```
</details>

## External Blog Posts
- [How to Deploy Storybook to GitHub Pages with GitHub Actions](https://www.bitovi.com/blog/deploy-storybook-to-github-pages-with-github-actions)

## Contributing
We would love for you to contribute to [`bitovi/github-actions-storybook-to-github-pages`](hhttps://github.com/bitovi/github-actions-storybook-to-github-pages).   [Issues](https://github.com/bitovi/github-actions-storybook-to-github-pages/issues) and [Pull Requests](https://github.com/bitovi/github-actions-storybook-to-github-pages/pulls) are welcome!

## License
The scripts and documentation in this project are released under the [MIT License](https://github.com/bitovi/github-actions-storybook-to-github-pages/blob/main/LICENSE).

# Provided by Bitovi
[Bitovi](https://www.bitovi.com/) is a proud supporter of Open Source software.

# We want to hear from you.
Come chat with us about open source in our Bitovi community [Discord](https://discord.gg/J7ejFsZnJ4Z)!
