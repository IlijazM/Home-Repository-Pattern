# Home Repository Pattern

A Home Repository is a waypoint: an AI coding agent passes through it on its way to the work and picks up what applies from there on.

It holds instructions, skills and knowledge.

It fixes drift: each piece lives in exactly one place instead of in copies across repositories.

It sets scope and access: where a piece lives decides what it applies to and who may see it.

## Pointers

A Home Repository points to the repositories the agent may go to next. A pointer is a short entry that says:

- what the repository is,
- which tasks belong there,
- where it lives (see [Repository locations](#repository-locations)), and how to reach it when that takes more than a clone.

A pointer never copies the target's content. The target stays the only source of truth for what it holds.

To follow pointers:

1. Decide which pointer matches the task.
2. Go to that repository (see [Going to a repository](#going-to-a-repository)) and read its instructions first.
3. If it is another Home Repository, repeat until you reach the repository that needs the change.
4. Make the change there, following that repository's own instructions.
5. No pointer matches, or several do: ask.

## Propagation

Pointers chain Home Repositories from the general to the specific. The agent starts at the top and keeps what every Home Repository on its way holds. This is **propagation**: whatever a Home Repository holds applies to everything below it. A lower Home Repository adds and narrows; it never repeats what a higher one already says.

An example chain. Every level is optional, and one Home Repository may cover several:

| Level | Holds, for example |
| --- | --- |
| Person | Personal writing style, commit identity |
| Person in an organization | How this person reaches the organization |
| Organization | What everyone in the organization needs, such as approaches from its wiki |
| Client | What the organization knows about a client and the client must not see, such as preferred code presentation |
| Client project | What the organization knows about one project, such as how agents reach the client's internal project wiki |
| Client project repository | Skills and instructions kept out of the client's repository itself |

## Permissions

Every Home Repository is an ordinary repository with its own access rights. Whoever can read it sees all of it, and so does every agent working for them. That makes the access rights the permission model:

- **Content goes where its readers are exactly right.** Put each instruction, skill or piece of knowledge into the Home Repository whose readers are exactly the people allowed to see it.
- **Pointers are visible, targets may not be.** A pointer can be read by everyone who can read its Home Repository, even when they cannot read the target. Point to a repository only where its existence may be known.
- **Agents read as their person.** An agent follows only pointers its person can read. Report missing access; never work around it.

## Purposes do not mix

Each Home Repository serves one audience: a person, an organization, a client or a project.

- No personal details in an organization's Home Repository.
- Nothing confidential about a client in anything that client can read.

## Rules for every Home Repository

- Start with: "This is a Home Repository, as defined in <https://github.com/IlijazM/Home-Repository-Pattern>."
- Never restate this definition. Link to it.
- List every repository it points to, with what it is and its location.
- Keep it current: when repositories or their locations change, update it in the same change.

## Repository locations

Every repository lives at:

```
~/repositories/<git-host>/<user-or-org>/<repository-name>
```

`~` is the home directory of the current user. Examples of `<git-host>`: `github.com`, `gitlab.com`, or a self-hosted GitLab.

## Going to a repository

In Claude Code on the web, attach GitHub repositories through the GitHub integration (e.g. `add_repo`) instead of cloning them. Everything else, and anything only reachable from a private network, goes through the steps below.

1. Check whether it is cloned at its location.
2. If it is, use it, after pulling the latest state where that is safe.
3. If not, clone it to exactly that location.
4. If it is only reachable from a private network (a VPN, an internal host), clone it and work on a machine inside that network. The pointer says how to get there.
5. If a location, host or machine named by a pointer no longer exists, tell the person instead of guessing.
