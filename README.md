This authenticates to Google Cloud and then Google Artifact Registry.

# What it does

* Auth to Google Cloud (getting an access token)
* Auth to Google Artifact Registry (`us-docker.pkg.dev`)
* Enable PyPI on Google Artifact Registry

# How to use it

```yaml
      - name: Auth to Google
        uses: 'uwit-iam/action-auth-artifact-registry@main'
        with:
          credentials: "${{ secrets.MCI_GCLOUD_AUTH_JSON }}"
          # REQUIRED if you want private GAR container registry access
          enable_private_docker: true
          # REQUIRED if you want private GAR PyPI access
          enable_private_pypi: true
```
