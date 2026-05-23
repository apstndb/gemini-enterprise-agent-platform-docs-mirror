# Gemini Enterprise Agent Platform Documentation Mirror

A local Markdown mirror of the [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/) documentation, automatically updated via GitHub Actions.

## Setup Instructions

1.  **Create a new repository** using this template.
2.  **Configure GitHub Secrets**:
    *   Go to `Settings` -> `Secrets and variables` -> `Actions`.
    *   Add a **New repository secret**:
        *   Name: `DEVELOPERKNOWLEDGE_API_KEY`
        *   Value: Your Google Cloud Developer Knowledge API Key.
    *   Alternatively, configure `GCP_WORKLOAD_IDENTITY_PROVIDER` and `GCP_SERVICE_ACCOUNT` for OIDC-based authentication.
3.  **Enable GitHub Actions**:
    *   Go to the `Actions` tab and enable workflows.
    *   The mirror updates daily at 16:30 UTC (01:30 JST), or you can trigger it manually via `workflow_dispatch`.

## Quota Management

The `gcp-docs-mirror-tools` is configured to respect quota limits, but simultaneous runs of multiple repositories will bypass these safety mechanisms. The cron in this repository is offset (16:30 UTC) to avoid colliding with other mirrors sharing the same API key.

## Manual Run

If you have Go installed locally, you can run the mirror script manually:

```bash
export DEVELOPERKNOWLEDGE_API_KEY=your_api_key
./mirror.sh
```

## Credits

This mirror system is powered by [gcp-docs-mirror-tools](https://github.com/apstndb/gcp-docs-mirror-tools).

## License

The documentation content collected in this repository is mirrored from Google Cloud Documentation according to the [Google Developers Site Policies](https://developers.google.com/terms/site-policies).
- Documentation content is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- Code samples are licensed under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0).
