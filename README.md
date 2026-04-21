# certifieddata-openapi

Public **OpenAPI 3.1 specification** and **Postman collection** for the CertifiedData API. Use this as a drop-in for SDK codegen, tool integrations (Zapier, n8n, Retool), and auditor-friendly contract review.

> CertifiedData is the certificate authority for AI artifacts — one Ed25519 signing root across Decision Ledger, Agent Commerce, and Dataset Generation. This spec covers the public and authenticated surfaces used by all three pillars.

## What's here

```
.
├── spec/
│   └── openapi.yaml                              # OpenAPI 3.1 spec — machine-readable contract
├── postman/
│   └── certifieddata.postman_collection.json     # Postman collection for humans
└── .github/workflows/
    └── lint.yml                                   # Spectral lint on every push
```

## Using the spec

### Generate a client SDK

```bash
# e.g. with openapi-generator
openapi-generator-cli generate \
  -i spec/openapi.yaml \
  -g typescript-fetch \
  -o ./sdk-ts

# or Python
openapi-generator-cli generate -i spec/openapi.yaml -g python -o ./sdk-py
```

### Import into Postman

Open Postman → **Import** → select `postman/certifieddata.postman_collection.json`. Set the `api_key` collection variable to your CertifiedData key. The anonymous endpoints (demo sign, public verify, sandbox key) work without a key.

### Mock locally with Prism

```bash
npx @stoplight/prism-cli mock spec/openapi.yaml
```

### Lint locally

```bash
npm i -g @stoplight/spectral-cli
spectral lint spec/openapi.yaml
```

## Scope notes

This spec intentionally covers the **stable public surface**. Internal admin endpoints, migration endpoints, and metabot internals are out of scope and will not appear here.

Versioning follows semver on the `info.version` field. Breaking changes to the public surface will bump the major version and be announced on the CertifiedData changelog.

## Contributing

1. Edit `spec/openapi.yaml`
2. Run `spectral lint spec/openapi.yaml` (CI runs the same)
3. Open a PR

## License

MIT — see [LICENSE](./LICENSE).
