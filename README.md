# New Org Template

This template quickstarts the ability of onboarding a new Salesforce org. Quickly get started and enable:

- Relevant Metadata Download
- Deployment Pipeline with GitHub Actions
- Prettier Config
![image](https://github.com/user-attachments/assets/35a49aca-e49e-4e55-a041-98842c81987e)

## Downloading Metadata From Salesforce

1. Open VS Code
2. Authenticate with Salesforce using the `sf` CLI.
3. Open the `manifest` folder.
4. Right click on the `package.xml` and select `SFDX: Retrieve Source in Manifest from Org`
5. Delete the `.gitkeep` file inside the `force-app` directory.

Allow the Metadata API to run and download source data from Salesforce. Customize the `package.xml` as needed for your needs. For more information check out this [video](https://youtu.be/SDFRU_-YZjk) on how to use the metadata api.

## Configuring A Deployment Pipeline

Github actions come as default to enable a deployment pipeline. To enable pushing from a `staging` branch to production:

1. Authenticate with `sf cli` using the following command: `sf org display --verbose --json -o <MY_TARGET_ORG_ALIAS>`.
2. Copy this value and add to the GitHub variable `SFDX_AUTH_URL`.
3. Ensure the target branch name is correct. The default branch is `master`.

To add additional environments, clone the `deploy-production.yml` and `validate-production.yml`. To learn more about using a developer pipeline, check out the following [tutorial](https://youtu.be/R31DWnkiYpY).

## Deploy Conga Composer

We can use [SFDMU](https://github.com/forcedotcom/SFDX-Data-Move-Utility) to move data from Sandbox to Production (Or Vice-Versa).

### Configuration

[Full Tutorial Here](https://www.1sync.co/deploy-conga-composer-production)

There are two files that need to be updated in the `conga/scripts` folder:

- `push-prod.sh`
- `refresh-sb.sh`

Replace `SB_USERNAME` with your Sandbox Alias, and `PROD_USERNAME` with your Production Alias.

Then, to push changes to production, run:

```bash
cd scripts/conga
sh push-prod.sh
```

or to refresh sandbox:

```bash
cd scripts/conga
sh refresh-sb.sh
```

## Backup Salesforce Metadata

We can backup the salesforce metadata nighly (or on-demand) using Github Actions.

Learn more by following [this](https://www.1sync.co/backup-salesforce-metadata-free) tutorial.

To set the time of the backup, edit this cron expression.

```yml
- cron: "0 0 * * *"
```

This will run every night at 12am (00:00) UTC.

## Code Formatting

This template uses the prettier and prettier-apex plugins to auto format.

To configure:

```bash
npm install
```
