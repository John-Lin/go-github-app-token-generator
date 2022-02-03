# Golang github app installation access token generator action

A simple github action written in go to retrieve an installation access token for an app installed into an organization.
There are a lot of other workflows that do the same thing, go use them instead. I created this as I wanted to do it purely in golang.

# Setup

This action requires three environment variables as inputs.

- `APP_PRIVATE_KEY`: base64 encoded private key
- `APP_ID`: application id
- `APP_INSTALLATION_ID`: application installation id

## Usage

```yaml
name: Checkout repos
on: push
jobs:
  checkout:
    runs-on: ubuntu-latest
    steps:
    - uses: mlioo/go-github-app-token-gen@v1
      id: get-token
      with:
        app-private-key: ${{ secrets.APP_PRIVATE_KEY }}
        app-id: ${{ secrets.APP_ID }}
        app-installation-id: ${{ secrets.APP_INSTALLATION_ID}}
    - name: Check out an other repo
      uses: actions/checkout@v2
      with:
        repository: owner/repo
        token: ${{ steps.get-token.outputs.token }}
```
