# Home Repository Pattern

The definition of a **Home Repository**. Every Home Repository links here instead of explaining the pattern itself, so the definition (paths above all) lives in exactly one place.

## What a Home Repository is

A Home Repository is a central repository that holds what an AI coding agent needs before it touches a project: instructions (`AGENTS.md`), skills and shared docs. Instead of copying them into every project, where they drift apart, they live in the Home Repository and are shared.

- It **points** to other repositories: one short entry per repository, saying what it is and where it lives.
- Each project repository keeps its own specific context. The Home Repository never copies it.
- Home Repositories **nest**: one may point to further Home Repositories, each adding context, until the project repository is reached. Example: personal Home Repository → work Home Repository → customer Home Repository → project repository.
- One session can work across several repositories.

## Two kinds

- **Personal Home Repository:** one per person, and the place where every session starts. Holds what is about that person: name, commit identity, language preferences, personal servers and accounts, and pointers to everything the person works on.
- **Organization Home Repository:** shared by everyone who works in that organization (a company, a customer, an agency). Holds only what is true for every contributor: the organization's projects, servers, rules and tools. Nothing personal, because each contributor brings that from their own personal Home Repository.

## Rules for every Home Repository

- Start with one line that names its kind and links here, e.g. "This is an organization Home Repository, as defined in <https://github.com/IlijazM/Home-Repository-Pattern>." Never restate this definition or the repository paths.
- List every repository it points to, with what it is and its location.
- List every server it needs and keep the list current. When a server is gone, tell the person instead of guessing.
- Keep it current: when repositories, servers or locations change, update it in the same change.

## Repository locations

Every repository lives at:

```
~/repositories/<git-host>/<user-or-org>/<repository-name>
```

`~` is the home directory of the current user. Examples of `<git-host>`: `github.com`, `gitlab.com`, or a self-hosted GitLab.

## Working from a Home Repository

1. Read the task and decide which area it belongs to.
2. Follow the matching pointer. If it leads to another Home Repository, read its `AGENTS.md` first, and keep following pointers until you reach the repository that needs the change.
3. Make the change there, following that repository's own `AGENTS.md`/`CLAUDE.md`.
4. If the task is ambiguous about which repository is meant, ask.

### Going to a repository

1. Check whether it is cloned at its location (see above).
2. If it is, use it, after pulling the latest state where that is safe.
3. If not, clone it to exactly that location.
4. If it is behind a **VPN**, clone and work on the server that has the VPN. The Home Repository that points to it says which server that is.

In Claude Code on the web, attach GitHub repositories through the GitHub integration (e.g. `add_repo`) instead of cloning. Other hosts have to be cloned.
