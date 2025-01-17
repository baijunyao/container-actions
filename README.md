# GitHub Actions for Containers
[GitHub Actions](https://help.github.com/en/articles/about-github-actions)  gives you the flexibility to build an automated software development lifecycle workflow. 

This repository contains GitHub Actions to [log in to a private container registry](https://docs.docker.com/engine/reference/commandline/login/) such as [Azure Container registry](https://azure.microsoft.com/en-us/services/container-registry/). Once login is done, the next set of Actions in the workflow can perform tasks such as building, tagging and pushing containers.

[GitHub Actions for Kubernetes](https://github.com/Azure/k8s-actions) contains actions for deploying to a Kubernetes cluster for example [Azure Kubernetes service (AKS)](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes). Similarly, there are actions for deploying to [Azure Web App for Containers](https://github.com/Azure/appservice-actions).

[GitHub Action for Azure repository](https://github.com/Azure/actions) has a list of all the GitHub Actions for Azure.

## Usage
Detailed usage information for individual commands can be found in their respective directories.

### Prerequisite
Get the username and password of your container registry and create secrets for them. For Azure Container registry refer to **admin [account document](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-authentication#admin-account)** for username and password.

Now add the username and password as [a secret](https://help.github.com/en/articles/virtual-environments-for-github-actions#creating-and-using-secrets-encrypted-variables) in the GitHub repository.

#### Example - Log in to a container registry
```yaml
- uses: azure/container-actions/docker-login@master
  with:
    username: '<username>'
    password: '<password>'
    loginServer: '<login server>' # default: index.docker.io
    email: '<email id>'
```

##### You can build and push container registry by using the following example
```yaml
- uses: azure/container-actions/docker-login@master
      with:
        login-server: contoso.azurecr.io
        username: ${{ secrets.REGISTRY_USERNAME }}
        password: ${{ secrets.REGISTRY_PASSWORD }}
    
    - run: |
        docker build . -t contoso.azurecr.io/k8sdemo:${{ github.sha }}
        docker push contoso.azurecr.io/k8sdemo:${{ github.sha }}
```

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
