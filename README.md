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

# Other important information

Enabling the private PyPI repo involves installing a Python package. This will be installed via `pip`.

Users of this action should **pre-configure the runner** as appropriate prior to calling this.

Likely that means calling e.g., [actions/setup-python to set the correct default Python version](https://github.com/actions/setup-python)


```yaml
      - uses: actions/setup-python@v5
        with:
          # auto-detect Python version from file; alternatively you can set to explicit version if desired
          python-version-file: pyproject.toml
```
