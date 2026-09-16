# Contributing to info-subscription-ai

Thanks for your interest in contributing plugins, marketplace entries,
skills, or instructions to this repo.

## Before you contribute

- Open an issue first for anything non-trivial (new plugin, new ecosystem
  support, breaking changes to a manifest) so we can align on approach.
- Keep changes scoped — one plugin/ecosystem/skill per PR where practical.
- Don't commit secrets, API keys, or tokens in any manifest, script, or doc.
- Match the existing structure: a new plugin goes in `plugins/<name>/` and
  gets an entry added to each relevant root `marketplace.json`; a new skill
  goes in `skills/<name>/SKILL.md`.

## Developer Certificate of Origin (DCO)

This project requires every commit to be signed off under the
[Developer Certificate of Origin (DCO) 1.1](https://developercertificate.org/).
Signing off means you certify:

> By making a contribution to this project, I certify that:
>
> (a) The contribution was created in whole or in part by me and I have the
>     right to submit it under the open source license indicated in the file;
>     or
> (b) The contribution is based upon previous work that, to the best of my
>     knowledge, is covered under an appropriate open source license and I
>     have the right under that license to submit that work with
>     modifications, whether created in whole or in part by me, under the
>     same open source license (unless I am permitted to submit under a
>     different license), as indicated in the file; or
> (c) The contribution was provided directly to me by some other person who
>     certified (a), (b) or (c) and I have not modified it.
> (d) I understand and agree that this project and the contribution are
>     public and that a record of the contribution (including all personal
>     information I submit with it, including my sign-off) is maintained
>     indefinitely and may be redistributed consistent with this project or
>     the open source license(s) involved.

Add a `Signed-off-by` trailer to every commit, either with:

```bash
git commit -s -m "Your commit message"
```

or by adding the line manually:

```
Signed-off-by: Your Name <your.email@example.com>
```

Use your real name and a reachable email address (no anonymous or pseudonymous
sign-offs). Pull requests with unsigned commits will be asked to amend and
force-push before merge.

## License

By contributing, you agree that your contribution is licensed under the
[MIT License](./LICENSE) that covers this repository (manifests, marketplace
catalogs, docs, skills, and instructions). Note this license covers the
*packaging/integration code in this repo* — it does not grant any rights to
the INFO-Subscription service or MCP server itself, which remains subject to
Infosoft's own terms.

## Pull request checklist

- [ ] Commits are signed off (`git commit -s`)
- [ ] Manifest changes validate against their ecosystem's schema (see each
      plugin's `README.md` for the relevant `marketplace update`/`upgrade`
      command to test locally)
- [ ] No secrets or credentials committed
- [ ] Relevant `README.md`/`LISTING.md` updated if behavior or install steps
      changed
