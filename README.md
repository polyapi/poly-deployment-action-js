# Poly Deployment Action

This GitHub Action automates the deployment process for all PolyAPI deployables in your application.

## Usage

To use this action in your workflow install it from the Github marketplace for actions.

Ensure you have the following secret variables defined within your github organization or within your github repository:

`POLY_API_KEY_PROD` - Your key to your production instance of PolyAPI.

`POLY_API_BASE_URL_PROD` - The base url to your production instance of PolyAPI, ex. `https://na1.polyapi.io` for north american cloud users.

`POLY_API_KEY_DEV` - Your key to your development instance/environment of PolyAPI.

`POLY_API_BASE_URL_DEV` - The base url to your development instance of PolyAPI, ex. `https://na1.polyapi.io` for north american cloud users.

Then copy the following and save it as `your_repo/.github/workflows/deploy.yml`:

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
        uses: polyapi/poly-deployment-action-js@v1
```

If you wish to set the api key or deploy url explicitly rather than letting the action pull them from secrets you may pass them along in your deploy step:

```yaml
    steps:
      - name: Poly Deploy
        uses: polyapi/poly-deployment-action-js@v1
        with:
          poly_api_key: ${{ secrets.CUSTOM_SECRET_KEY }}
          poly_api_base_url: https://my.poly.instance.com
```