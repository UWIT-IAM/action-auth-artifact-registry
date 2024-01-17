This authenticates to Google Cloud and then Google Artifact Registry.

# What it does

* Auth to Google Cloud (getting an access token)
* Auth to Google Artifact Registry (`us-docker.pkg.dev`)

# How to use it

```yaml
      - name: Auth to Google
        uses: 'uwit-iam/action-auth-artifact-registry@main'
        with:
          pypi: "${{ vars.IAM_GAR_PYPI }}"
          credentials: "${{ secrets.MCI_GCLOUD_AUTH_JSON }}"
```
