# <img src="https://polyapi.io/wp-content/uploads/2024/05/poly-block-logo-mark.png" height="24px"/> PolyAPI Deployment Action

This GitHub Action automates the deployment process for all PolyAPI deployables in your application.

PolyAPI accelerates development and simplifies the operation of integrations, orchestrations, and microservices with TypeScript, Python, Java, and C#, built on Kubernetes-native technology and cutting-edge AI.

PolyAPI documentation: https://docs.polyapi.io/

Learn more about Poly: https://polyapi.io/

## Usage

To use this action in your workflow:
1. Install it from the Github marketplace for actions.

2. Ensure you have the following secret variables defined within your github organization or within your github repository:

    `POLY_API_KEY` - Your key to your instance of PolyAPI.

    `POLY_API_BASE_URL` - The base url to your instance of PolyAPI, ex. `https://na1.polyapi.io` for north american cloud users.

3. Then copy the following and save it as `your_repo/.github/workflows/deploy.yml`:

    ```yaml
    name: Deploy to PolyAPI
    on:
      push:
        branches:
          - main

    concurrency:
      group: ${{ github.ref }}
      cancel-in-progress: true

    jobs:
      deploy:
        runs-on: ubuntu-latest

        steps:
          - name: Poly Deploy
            uses: polyapi/poly-deployment-action-js@v0.2.9-alpha
            with:
              poly_api_key: ${{ secrets.POLY_API_KEY }}
              poly_api_base_url: ${{ secrets.POLY_API_BASE_URL }}
    ```