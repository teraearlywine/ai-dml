# October 2026 eMudhra TLS response

The requirements lock pinned certifi 2025.1.31. Update it to 2026.10.19 for the OpenAI/HTTPX clients used by the DML agents.

The incident concerns compromised intermediate signing keys, not a leaked private key belonging to this repository. No known incident certificate was found in the repository scan; an old trust bundle can still accept certificates issued through the compromised intermediates.

Update every installed package installer: pip must be >=26.2.2 and uv, if installed, must be >=0.13.4. Updating certifi or uv does not replace pip's private CA bundle. Remove or retire unused older installers so they cannot be invoked later.

The pip bootstrap below requires Python >=3.10. For an older interpreter, stop using its pip for network installs and retire that environment; install a maintained Python release through a trusted, integrity-verified distribution channel, recreate the environment, bootstrap pip there, then reinstall and test this project. This does not claim that legacy Python environments are remediated. For Python >=3.10, run the PSF's hash-verified bootstrap with each environment's own Python:

```sh
python -m pip install --upgrade --no-deps 'https://files.pythonhosted.org/packages/3f/06/3e4420302363fbb71be3c7f35ce042f54bfca330e3e66b3a2e3c4cca579f/pip-26.2.2-py3-none-any.whl#sha256=fd7f4dfa8190e014013b9f08f3e973f4e4c26ffd179a204895533a7254813a70'
```

After bootstrapping pip, upgrade any installed uv with `python -m pip install --upgrade 'uv>=0.13.4'`; check `python -m pip --version` and every `uv --version` on PATH. Recheck newly created environments because ensurepip may seed an older pip.

Recreate or update environments, rebuild images, restart processes, and verify the installed bundle before treating a running deployment as remediated. This PR does not deploy anything. Inspect OS trust and any SSL_CERT_FILE, SSL_CERT_DIR, REQUESTS_CA_BUNDLE, or custom TLS context independently; repository changes cannot prove deployed settings. Unused or future clients that choose their own CA bundles need their own verification.

Sources: [certifi 2026.10.19](https://github.com/certifi/python-certifi/releases/tag/2026.10.19), [Python Security Response Team guidance](https://discuss.python.org/t/information-for-python-users-regarding-emudhra-emsign-ca-certificate-security-incident/109576).
