# October 2026 eMudhra TLS response

The requirements lock pinned certifi 2025.1.31. Update it to 2026.10.19 for the OpenAI/HTTPX clients used by the DML agents.

The incident concerns compromised intermediate signing keys, not a leaked private key belonging to this repository. No known incident certificate was found in the repository scan; an old trust bundle can still accept certificates issued through the compromised intermediates.

Before reinstalling requirements, use pip >=26.2.2 or uv >=0.13.4. For an existing virtual environment, the PSF supplies this hash-verified pip bootstrap (run with that environment's Python):

```sh
python -m pip install --upgrade --no-deps 'https://files.pythonhosted.org/packages/3f/06/3e4420302363fbb71be3c7f35ce042f54bfca330e3e66b3a2e3c4cca579f/pip-26.2.2-py3-none-any.whl#sha256=fd7f4dfa8190e014013b9f08f3e973f4e4c26ffd179a204895533a7254813a70'
```

Recreate or update environments, rebuild images, restart processes, and verify the installed bundle before treating a running deployment as remediated. This PR does not deploy anything. Inspect OS trust and any SSL_CERT_FILE, SSL_CERT_DIR, REQUESTS_CA_BUNDLE, or custom TLS context independently; repository changes cannot prove deployed settings. Unused or future clients that choose their own CA bundles need their own verification.

Sources: [certifi 2026.10.19](https://github.com/certifi/python-certifi/releases/tag/2026.10.19), [Python Security Response Team guidance](https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576).
