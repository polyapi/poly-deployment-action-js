# <img src="https://polyapi.io/wp-content/uploads/2024/05/poly-block-logo-mark.png" height="24px"/> PolyAPI Deployment Action

This GitHub Action automates the deployment process for all PolyAPI deployables in your application.

PolyAPI accelerates development and simplifies the operation of integrations, orchestrations, and microservices with TypeScript, Python, Java, and C#, built on Kubernetes-native technology and cutting-edge AI.

PolyAPI documentation: https://docs.polyapi.io/

Learn more about Poly: https://polyapi.io/

## Usage

To use this action in your workflow:
1. Install it from the Github marketplace for actions.

2. Ensure you have the following secret variables defined within your github organization or within your github repository:

    `POLY_API_KEY_PROD` - Your key to your production instance of PolyAPI.

    `POLY_API_BASE_URL_PROD` - The base url to your production instance of PolyAPI, ex. `https://na1.polyapi.io` for north american cloud users.

    `POLY_API_KEY_DEV` - Your key to your development instance/environment of PolyAPI.

    `POLY_API_BASE_URL_DEV` - The base url to your development instance of PolyAPI, ex. `https://na1.polyapi.io` for north american cloud users.

3. Then copy the following and save it as `your_repo/.github/workflows/deploy.yml`:

    ```yaml
    name: Deploy to PolyAPI
    on:
      push:
        branches:
          - develop
          - main

    jobs:
      deploy:
        runs-on: ubuntu-latest
        concurrency:
          group: ${{ github.ref }}
          cancel-in-progress: true

        steps:
          - name: Poly Deploy
            uses: polyapi/poly-deployment-action-js@v0.2.2-alpha
    ```

### Setting keys explicitly

If you wish to set the api key or deploy url explicitly rather than letting the action pull them from secrets you may pass them along in your deploy step:

```yaml
    steps:
      - name: Poly Deploy
        uses: polyapi/poly-deployment-action-js@v0.2.2-alpha
        with:
          poly_api_key: ${{ secrets.CUSTOM_SECRET_KEY }}
          poly_api_base_url: https://my.poly.instance.com
```

### No development environment?

Straight to prod? We can handle that.

Continue to use `main` as your production branch and define `POLY_API_KEY_PROD` and `POLY_API_BASE_URL_PROD` as secrets in github.

Modify your `your_repo/.github/workflows/deploy.yml` to only deploy on push to main:
```yaml
name: Deploy to PolyAPI
on:
  push:
    branches:
      - main
```