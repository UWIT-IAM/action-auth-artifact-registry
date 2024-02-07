This authenticates to Google Cloud and then Google Artifact Registry.

# What it does

* Auth to Google Cloud (getting an access token)
* Auth to Google Artifact Registry (`us-docker.pkg.dev`)
* Enable PyPI on Google Artifact Registry by installing an appropriate keyring via `pip`
    * This **does not integrate with poetry** if you are using `pipx`. For that you can
        * Manually run ` poetry self add keyrings.google-artifactregistry-auth`
        * PR an extra input to this action (or ask @miker985 to do it)

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

# Outputs

These outputs are all provided by the underling [google-github-actions/auth action's outputs](https://github.com/google-github-actions/auth?tab=readme-ov-file#outputs)

* `project_id`: Provided or extracted value for the Google Cloud project ID.
* `credentials_file_path`: Path on the local filesystem where the generated credentials file resides.
* `auth_token`: The Google Cloud federated token (for Workload Identity Federation) or self-signed JWT (for a Service Account Key JSON).
* `access_token`: The Google Cloud access token for calling other Google Cloud APIs.

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
