# Changelog

## [1.4.0](https://github.com/opencrvs/opencrvs-countryconfig/compare/v1.3.3...v1.4.0) (TBD)

- Added examples for configuring HTTP-01, DNS-01, and manual HTTPS certificates. By default, development and QA environments use HTTP-01, while others use DNS-01.
- All secrets & variables defined in Github Secrets are now passed automatically to the deployment script.
- The VPN_HOST_ADDRESS variable is now required for staging and production installations to ensure deployments are not publicly accessible.
- Replica limits have been removed; any number can now be deployed.
- Each environment now has a dedicated docker-compose-<environment>-deploy.yml. Use `environment:init` to create a new environment and generate a corresponding file for customizable configurations.
- 🔒 OpenHIM console is no longer exposed via HTTP.
- Ansible playbooks are refactored into smaller task files.

### New features

- We now recommend creating a new Ubuntu user `provision` with passwordless sudo rights for all automated operations on the server, instead of using the root user. New users for different operations will be created in future releases.
- All human users on all servers now have their own Linux users with mandatory 2-factor authentication.
- OpenCRVS Farajaland now has an interactive script `environment:init` for creating new Github environments and defining secrets. This script should also be run for existing environments to ensure all variables and secrets are defined, especially important when pulling the latest changes from the Farajaland repository to your own country resource package.
- The environment creator script also manages the known hosts file automatically.
- 🚰 New pipeline for automatic provisioning of Ubuntu servers (all environments).
- 🚰 New pipeline for resetting data from an environment (non-production environments).
- 🚰 New pipeline for resetting SSH 2FA for all environments.
- 🚰 Development deploy pipeline now includes a "debug" option for SSHing into the action runner (non-production environments).
- A new "staging" environment has been introduced, acting as a production environment clone that resets its data nightly to match the production environment.
- The deployment script can now verify if there are undefined environment variables referred to in your compose files. All secrets and variables defined in Github Environments are automatically passed down to the deployment script.
- 🔒 Backup archives are now secured with a passphrase.
- HTTPS setup now offers three options: HTTP challenge, DNS challenge, and using a pre-issued certificate file.
- There's now a generic purpose POST /email endpoint only available from the internal network. Elastalert2 is configured to use this endpoint instead of directly using SMTP details or the Sendgrid API key.
- 🔒 QA environment now hosts a Wireguard server and admin panel (wg-easy). After deploying, you can access the admin panel at vpn.<your domain>.
- Allow configuring additional SSH parameters globally using `SSH_ARGS` Github variable.

### Breaking changes

- Known hosts are now defined in the `infrastructure/known-hosts` file. You can clear the file and use `bash infrastructure/environments/update-known-hosts.sh <domain>` to add your own domains.
- Ansible inventory files are now in .yml format. Please convert your old `production.ini` and similar files to this new format.
- The `authorized_keys` file has been removed, and keys should now be defined in the inventory yaml files.
- The `DOCKER_PASSWORD` secret has been replaced with `DOCKER_TOKEN`.

### Note

In the next OpenCRVS release v1.5.0, there will be two significant changes:

- The `infrastructure` directory and related pipelines will be moved to a new repository.
- Both the new infrastructure repository and the OpenCRVS country resource package repositories will start following their own release cycles, mostly independent from the core's release cycle. From this release forward, both packages are released as "OpenCRVS minor compatible" releases, meaning that the OpenCRVS countryconfig 1.3.0-<incrementing release number> is compatible with OpenCRVS 1.3.0, 1.3.1, 1.3.2, etc. This allows for the release of new hotfix versions of the core without having to publish a new version of the infrastructure or countryconfig.

See [Releases](https://github.com/opencrvs/opencrvs-countryconfig/releases) for release notes of older releases.

## [1.3.3](https://github.com/opencrvs/opencrvs-countryconfig/compare/v1.3.2...v1.3.3) (TBD)

### Breaking changes

### New features

### Bug fixes

See [Releases](https://github.com/opencrvs/opencrvs-countryconfig/releases) for release notes of older releases.
