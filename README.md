# Rotate keys with ComplyRobin

This repository runs the [ComplyRobin rotation runner](https://github.com/complyrobin/runner) every hour. It swaps the API keys ComplyRobin says are due, in your own accounts, and reports back. Your keys and admin tokens stay here, in your GitHub secrets: ComplyRobin never sees them.

## Set it up

1. Make sure this repository is **private**.
2. Go to **Settings, Secrets and variables, Actions** and add these repository secrets. Only the first is always needed; add the rest for the services you use.

   | Secret | What it is |
   | --- | --- |
   | `COMPLYROBIN_TOKEN` | The runner token (`crr_…`). Already here if ComplyRobin made this repository for you; otherwise the token ComplyRobin showed you once. |
   | `OPENAI_ADMIN_KEY` | To rotate OpenAI keys: an OpenAI admin key that can manage API keys. |
   | `GOOGLE_CLOUD_CREDENTIALS` | To rotate Google Cloud keys: the JSON key file of a service account that can manage keys. |
   | `LARAVEL_CLOUD_API_TOKEN` | To put keys in Laravel Cloud: an API token that can update secrets and deploy. |
   | `GH_SECRETS_TOKEN` | To put keys in GitHub secrets: a token that can write the target repository's secrets. |
   | `FORGE_API_TOKEN` | To put keys in a Laravel Forge site: a Forge API token. |
   | `VERCEL_TOKEN` | To put keys in Vercel: a Vercel token. |

   Rotating AWS keys? Sign in with a role instead of a stored key: remove the `#` signs in front of the AWS step in `.github/workflows/rotate-keys.yml` and put in your role.

3. Test it: go to **Actions, Rotate keys, Run workflow**, choose `check` and run it. The results also show on the **Rotation runners** page in ComplyRobin.

That's all. The runner checks in every hour, and ComplyRobin decides what is due. On its first check-in it also sends ComplyRobin the names of the projects, apps and repositories your tokens can see (never a key), so you can pick them when you set up a credential.
