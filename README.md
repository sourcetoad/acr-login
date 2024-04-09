# Aliyun (Alibaba Cloud) Container Registry Login
_Forked from [aliyun/acr-login](https://github.com/aliyun/acr-login) to prevent manual creation of docker config file._

Use this GitHub Action to [log in to a private container registry](https://docs.docker.com/engine/reference/commandline/login/) of [Alibaba Cloud Container Registry](https://www.aliyun.com/product/acr). Once login is done, the next set of actions in the workflow can perform tasks such as building, tagging and pushing containers.

```yaml
- uses: aliyun/acr-login@v1
  with:
    login-server: '<login server>' # default: https://index.docker.io/v1/
    username: '<username>'
    password: '<password>'
```

Or

```yaml
- uses: aliyun/acr-login@v1
  with:
    region-id: '<region id>' # example: cn-hangzhou
    access-key-id: '<access key id>'
    access-key-secret: '<access key secret>'
```

Or

```yaml
- uses: aliyun/acr-login@v1
  with:
    login-server: '<login server>' # example: https://my-test-registry.cn-hangzhou.cr.aliyuncs.com
    region-id: '<region id>' # example: cn-hangzhou
    access-key-id: '<access key id>'
    access-key-secret: '<access key secret>'
    instance-id: '<registry instance id>'
```

Refer to the action metadata file for details about all the inputs: [action.yml](https://github.com/aliyun/acr-login/blob/master/action.yml)

## You can build and push container registry by using the following example
```yaml
- name: Login to ACR
  uses: aliyun/acr-login@v1
  with:
    login-server: https://registry.cn-hangzhou.aliyuncs.com
    username: "${{ secrets.REGISTRY_USERNAME }}"
    password: "${{ secrets.REGISTRY_PASSWORD }}"
- name: Build and push image
  env:
    IMAGE_TAG: ${{ github.sha }}
  run: |
    docker build -t registry.cn-hangzhou.aliyuncs.com/myrepo/demo:$IMAGE_TAG .
    docker push registry.cn-hangzhou.aliyuncs.com/myrepo/demo:$IMAGE_TAG
```

### Prerequisite
Get the username and password of your container registry or get the authentication token fo temporary access by access key. 

Now add the username and password or access key as [secrets](https://developer.github.com/actions/managing-workflows/storing-secrets/) in the GitHub repository.
