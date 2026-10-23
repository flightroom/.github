![Flightroom](banner.png)

# Flightroom

**Build apps and AI agents by describing them. Ship them in one click, inside
IT's rules.**

Flightroom is an open-source enterprise platform where anyone in a company can
describe the app or the agent they need. The AI writes the code in your own Git
repositories, your engineers review it, and one click deploys it to your
Kubernetes through GitOps and Argo CD — with your single sign-on, your roles and
your AI models.

🔗 **Website:** [flightroom.dev](https://flightroom.dev/) ·
📖 **Documentation:** [flightroom.dev/documentation](https://flightroom.dev/documentation/) ·
🖥️ **Hosted console:** [console.flightroom.dev](https://console.flightroom.dev/)

> Flightroom was previously called **MFE Orchestrator**. Same project, new name.

## How it works

1. **Describe it.** Write what the app or agent should do. Flightroom proposes
   the web interfaces and backend services it needs, and you adjust the
   proposal.
2. **The AI builds it in your repositories.** Each repository is created in your
   GitHub, GitLab or Azure DevOps from a Flightroom template, CI included, and
   the AI writes the first version on a branch.
3. **Your team reviews it.** Every AI change starts on its own branch and can be
   opened as a pull request, through your code review and your CI.
4. **One click ships it.** Deploying commits to Git, your Argo CD syncs it, and
   the app gets its own URL with TLS in every environment.

## What you get

- **Your stack** — web interfaces in React, Angular or Vue; services in Node.js,
  Python, Spring Boot or Quarkus. An agent is a service that calls your AI model,
  built, reviewed and deployed like any other.
- **GitOps and Argo CD** — every deploy is a Git commit; the console never holds
  cluster credentials. Dev, UAT, production or your own stages, each a
  Kubernetes namespace.
- **Immutable deployments, one-click rollback** — every deploy is a snapshot;
  rolling back re-activates the previous one.
- **Your sign-on and your roles** — Microsoft Entra ID, Google, Auth0 or local
  accounts, with organization and project roles. Viewers cannot request or apply
  AI changes.
- **Your AI models** — Claude through Anthropic, Azure AI Foundry or AWS
  Bedrock, GPT through Azure OpenAI, or Gemini, with your own credentials.
- **Frontends served by Flightroom** — when a web interface does not need its
  own container, Flightroom stores its builds, picks the version each
  environment serves and composes it into a host with Module Federation, with
  canary releases.
- **Your cloud** — self-host on your Kubernetes, in your cloud or on-premise.

## Get Flightroom

**Hosted — nothing to install.** Sign up free at
[console.flightroom.dev](https://console.flightroom.dev/).

**Self-hosted — one container.** The all-in-one image bundles Flightroom,
MongoDB, Redis and Nginx:

```bash
docker run -d --name flightroom --restart unless-stopped \
  -p 8080:80 -v flightroom-data:/data lory1990/flightroom:all-in-one
```

Open http://localhost:8080 and create the first user.

**Self-hosted — on Kubernetes.** The Helm chart is published on ghcr.io:

```bash
helm install flightroom oci://ghcr.io/flightroom/charts/flightroom \
  --namespace flightroom --create-namespace -f my-values.yaml
```

Docker Compose and a Terraform / OpenTofu template live in the
[main repository](https://github.com/flightroom/flightroom#self-hosting).

Whichever you choose, the
[**quick start**](https://flightroom.dev/documentation/docs/quick-start) takes
you from a description to an app in your repositories, and
[**deploy to Kubernetes**](https://flightroom.dev/documentation/docs/kubernetes/overview)
puts it in front of users.

## Use it from your AI client (MCP)

Flightroom runs a remote [MCP](https://modelcontextprotocol.io) server: Claude,
ChatGPT, Gemini, Claude Code, Cursor, VS Code and Gemini CLI can read your
projects, create and change frontends and services, and deploy, with your role
on each project. The client signs in with OAuth and you pick the projects it may
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
| [flightroom](https://github.com/flightroom/flightroom) | The platform: backend, console and self-hosting assets (Docker, Compose, Helm, Terraform) |
| [documentation](https://github.com/flightroom/documentation) | The documentation site — [flightroom.dev/documentation](https://flightroom.dev/documentation/) |
| [flightroom.github.io](https://github.com/flightroom/flightroom.github.io) | The public website — [flightroom.dev](https://flightroom.dev/) |
| [design-system](https://github.com/flightroom/design-system) | The shared React design system used by the console, the website and the docs |
| [template-service-node-fastify](https://github.com/flightroom/template-service-node-fastify) · [template-service-spring-boot](https://github.com/flightroom/template-service-spring-boot) · [template-service-quarkus](https://github.com/flightroom/template-service-quarkus) · [template-service-python-fastapi](https://github.com/flightroom/template-service-python-fastapi) | Templates the services and agents start from |

## Contribute

Every repository accepts pull requests: fork → branch → conventional commit →
pull request. The
[main README](https://github.com/flightroom/flightroom#contributing-) covers the
local development setup. Good places to start are issues labelled
[good first issue](https://github.com/flightroom/flightroom/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22),
the documentation, and new templates for the stacks we do not cover yet.

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
