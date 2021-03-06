# ServiceNow CI/CD GitHub Action for Install Application

Installs the specified application from the application repository onto the local instance.

### Requirements
- nodejs version >= 12
### DevDependecies
- [jest](https://github.com/facebook/jest)
- [prettier](https://github.com/prettier/prettier)
- [eslint](https://github.com/eslint/eslint)
- [ts-jest](https://github.com/kulshekhar/ts-jest)
- [typescript](https://github.com/microsoft/TypeScript)
- [@types/jest](https://www.npmjs.com/package/@types/jest)
- [@types/node](https://www.npmjs.com/package/@types/node)
- [@typescript-eslint/eslint-plugin](https://www.npmjs.com/package/@typescript-eslint/eslint-plugin)
- [@typescript-eslint/parser](https://www.npmjs.com/package/@typescript-eslint/parser)
- [eslint-config-prettier](npmjs.com/package/eslint-config-prettier)
- [eslint-plugin-prettier](https://www.npmjs.com/package/eslint-plugin-prettier)

### Dependencies
- [@actions/core](https://github.com/actions/toolkit/tree/master/packages/core)
- [@actions/github](https://github.com/actions/toolkit/tree/master/packages/github)
- [axios](https://github.com/axios/axios)

# Usage
## Step 1: Collect the data from ServiceNow
Collect all required data from the ServiceNow - username, password, instance, application sys_id or scope
## Step 2: Configure Secrets in your GitHub repository
On GitHub, go in your repository settings, click on the secret _Secrets_ and create a new secret.

Create secrets called 
- `SNOW_USERNAME`
- `SNOW_PASSWORD`
- `SNOW_INSTALL_INSTANCE` **domain** only required from the url like https://**domain**.service-now.com
- `APP_SYS_ID` or `APP_SCOPE`

## Step 3: Configure the GitHub action
```yaml
- name: Install Application 
  id: install_app # id of the step
  uses: ServiceNow/sncicd_install_app # like username/repo-name
  with:
    version: ${{steps.publish_app.outputs.newVersion}}
  env:
    snowUsername: ${{ secrets.SNOW_USERNAME }}
    snowPassword: ${{ secrets.SNOW_PASSWORD }}
    snowInstallInstance: ${{ secrets.SNOW_INSTALL_INSTANCE }}
    appSysID: ${{ secrets.APP_SYS_ID }}
    appScope: ${{ secrets.APP_SCOPE }}
```
Inputs:
- **version** - Application version to install. Takes the version from the publish application step. steps._**publish_app**_.outputs.newVersion is an id of the step
    
Outputs:
- **rollbackVersion** - The previously installed version.
    
Environment variable should be set up in the Step 1
- snowUsername - Username to ServiceNow instance
- snowPassword - Password to ServiceNow instance
- snowInstallInstance - ServiceNow instance where application will be installed
- appSysID - Required if app_scope is not specified. The sys_id of the application
- appScope - Required if app_sys_id is not specified. The scope name of the application, such as x_aah_custom_app

## Tests

Tests should be ran via npm commands:

#### Unit tests
```shell script
npm run test
```   

#### Integration test
```shell script
npm run integration
```   

## Build

```shell script
npm run buid
```

## Formatting and Linting
```shell script
npm run format
npm run lint
```
