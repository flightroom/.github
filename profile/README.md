![Flightroom, the open-source control room for micro frontends](banner.png)

# Flightroom

**The open-source control plane for micro frontends.** Flightroom stores every
build you publish, decides which version each environment serves, and hands
your host application the runtime configuration it needs — so releasing one
micro frontend never means rebuilding the shell.

🔗 **Website:** [flightroom.dev](https://flightroom.dev/) ·
📖 **Documentation:** [flightroom.dev/documentation](https://flightroom.dev/documentation/) ·
🖥️ **Hosted console:** [console.flightroom.dev](https://console.flightroom.dev/)

> Flightroom was previously called **MFE Orchestrator**. Same project, new name.

## What it does

Micro frontends promise independent deployment, but most setups still decide at
build time what the host loads: releasing one widget means rebuilding the shell,
and a rollback is a revert, a rebuild and a wait. Flightroom moves that decision
to runtime.

- **Independent releases** — publish a micro frontend, assign the version to an
  environment, press **Deploy**. The host application is untouched.
- **One-click rollback** — every deployment is an immutable snapshot; rolling
  back is re-activating the previous one. No rebuild, no pipeline wait.
- **One build, every environment** — per-environment variables reach the
  browser at boot, so the same artifact serves DEV, UAT and PROD.
- **Module Federation, configured for you** — the console generates the Vite or
  Webpack configuration your host needs.
- **Your storage, your rules** — artifacts live on the hub, in your own S3,
  Azure Blob or Google Cloud Storage bucket, on your CDN, or fully on-premise.
- **CI/CD included** — ready-made pipelines for GitHub Actions, GitLab CI and
  Azure DevOps, plus an API for everything else.
- **Canary releases** — roll out a new version to a percentage of traffic, a
  sticky share of browsers or an explicit list of users.

## Get Flightroom

**Hosted — nothing to install.** Sign up free at
[console.flightroom.dev](https://console.flightroom.dev/).

**Self-hosted — one container.** The all-in-one image bundles Flightroom,
MongoDB, Redis and Nginx:

```bash
docker run -d --name flightroom --restart unless-stopped \
  -p 8080:80 -v flightroom-data:/data flightroom/flightroom:all-in-one
```

Open http://localhost:8080 and create the first user.

**Self-hosted — production setups.** Clone the
[main repository](https://github.com/flightroom/flightroom) and pick the
deployment that fits your infrastructure:

```bash
git clone https://github.com/flightroom/flightroom.git
cd flightroom
docker compose up -d
```

A [Helm chart](https://github.com/flightroom/flightroom/tree/main/helm) for
Kubernetes and a
[Terraform / OpenTofu template](https://github.com/flightroom/flightroom/tree/main/terraform)
live in the same repository.

Whichever you choose, the
[**10-minute quick start**](https://flightroom.dev/documentation/docs/quick-start)
takes you from an empty project to a deployed micro frontend — and back with a
one-click rollback.

## Use it from your AI client (MCP)

Flightroom runs a remote [MCP](https://modelcontextprotocol.io) server: Claude,
ChatGPT, Gemini, Claude Code, Cursor, VS Code and Gemini CLI can read your
projects, manage micro frontends and services, and deploy, with your role on
each project. The client signs in with OAuth and you pick the projects it may
use.

**Server URL:** `https://console.flightroom.dev/api/mcp` — on a self-hosted
install, `https://<your console>/api/mcp`.

```bash
# Claude Code (then run /mcp to sign in)
claude mcp add --transport http flightroom https://console.flightroom.dev/api/mcp
```

```jsonc
// Cursor: ~/.cursor/mcp.json
{ "mcpServers": { "flightroom": { "url": "https://console.flightroom.dev/api/mcp" } } }

// VS Code: .vscode/mcp.json
{ "servers": { "flightroom": { "type": "http", "url": "https://console.flightroom.dev/api/mcp" } } }

// Gemini CLI: ~/.gemini/settings.json (then /mcp auth flightroom)
{ "mcpServers": { "flightroom": { "httpUrl": "https://console.flightroom.dev/api/mcp" } } }
```

In Claude, ChatGPT or Gemini, add the URL as a custom connector. Clients that
cannot do OAuth can send a project API key as `Authorization: Bearer <key>`.
Self-hosted installs turn the server on with `MCP_ENABLED=true` and their own
`JWT_SECRET`. Everything else is in the
[MCP server guide](https://flightroom.dev/documentation/docs/build-with-ai/mcp-server/).

## The repositories

| Repository | What it is |
| --- | --- |
| [flightroom](https://github.com/flightroom/flightroom) | The platform: backend, console and self-hosting assets (Docker, Compose, Terraform, Helm) |
| [documentation](https://github.com/flightroom/documentation) | The documentation site — [flightroom.dev/documentation](https://flightroom.dev/documentation/) |
| [flightroom.github.io](https://github.com/flightroom/flightroom.github.io) | The public website — [flightroom.dev](https://flightroom.dev/) |
| [design-system](https://github.com/flightroom/design-system) | The shared React design system used by the console, the website and the docs |
| [template-service-node-fastify](https://github.com/flightroom/template-service-node-fastify) · [template-service-spring-boot](https://github.com/flightroom/template-service-spring-boot) · [template-service-quarkus](https://github.com/flightroom/template-service-quarkus) · [template-service-python-fastapi](https://github.com/flightroom/template-service-python-fastapi) | Backend service templates |

## Contribute

Every repository accepts pull requests: fork → branch → conventional commit →
pull request. The
[main README](https://github.com/flightroom/flightroom#contributing-) covers the
local development setup. Good places to start are issues labelled
[good first issue](https://github.com/flightroom/flightroom/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22),
the documentation, and CI/CD adapters for the vendors we do not support yet
(Jenkins, Bitbucket Pipelines, CircleCI, …).

Using Flightroom and reporting what breaks is just as valuable: open an issue in
the repository concerned, or on
[.github](https://github.com/flightroom/.github/issues) if you are not sure
which one.

## License

The platform is licensed under
[Apache-2.0](https://github.com/flightroom/flightroom/blob/main/LICENSE); the
surrounding tooling and templates are MIT. Each repository carries its own
LICENSE file.

---

If Flightroom is useful to you, a
[⭐ on the main repository](https://github.com/flightroom/flightroom) helps the
project get found.
