# Granting ChatGPT Codex Access to a GitHub Repository

Use this checklist when a ChatGPT or Codex chat can see a public repository but cannot create files, commits, or issues—or reports `403`, `404`, or repository-access errors.

Public visibility does **not** automatically grant the ChatGPT Codex Connector write access. The repository must be included in the GitHub App installation.

## Direct configuration link

For the current `jmbjr` installation:

<https://github.com/settings/installations/152338690>

The installation ID is account-specific. If the link does not apply to the current GitHub account, use the navigation steps below.

## GitHub website steps

1. Sign in to the GitHub account that owns the repository.
2. Open the profile menu and select **Settings**.
3. Scroll to **Integrations**.
4. Select **Applications**.
5. Open the **Installed GitHub Apps** tab.
6. Find **ChatGPT Codex Connector**.
7. Select **Configure**.
8. Under **Repository access**, choose one of:
   - **All repositories** to grant access to all current and future repositories; or
   - **Only select repositories** for narrower access.
9. If using **Only select repositories**, open **Select repositories** and add every repository the chat must modify.
10. Confirm that the repository appears in the selected-repository list.
11. Select **Save**.

For the current family game projects, the selected list should include as needed:

- `jmbjr/horseracing`
- `jmbjr/Kuicks`

GitHub repository names are case-insensitive in URLs, but use the displayed repository spelling in documentation.

## After saving GitHub access

GitHub authorization and an already-running chat session may refresh at different times.

1. Return to ChatGPT/Codex.
2. Reconnect or refresh the GitHub connector if the application offers that option.
3. Reload the chat, start a new task, or create a new chat if the old session still reports the previous permission state.
4. Ask the chat to verify access with a small read operation first:

   ```text
   Use the GitHub connector to fetch README.md from jmbjr/<repository> and report whether access succeeds.
   ```

5. Before beginning substantial work, verify write access with the intended operation, such as creating an issue or a deliberately requested documentation file.

## Codex Cloud environments are separate

The GitHub App installation and a Codex Cloud environment are different permission layers.

| Layer | Purpose |
|---|---|
| GitHub App installation | Grants the ChatGPT Codex Connector repository permissions |
| ChatGPT GitHub connector | Gives the current chat GitHub tools |
| Codex Cloud environment | Provides the runtime, setup, cache, and network policy for a coding task |

If a Codex Cloud task needs to clone or contact GitHub from its shell:

1. Open the Codex environment.
2. Select **Edit**.
3. Enable **Agent internet access** when direct network access is required.
4. Save the environment.
5. Select **Reset cache** when a prior setup was cached without the required access.
6. Restart the task using that environment.

Enabling environment internet access does not replace GitHub App authorization for authenticated writes.

## Error guide

### `403 Forbidden`

Usually means one of:

- The GitHub App is installed but the repository is not selected.
- The connector has read access but not the required write permission.
- The Codex environment cannot reach GitHub because agent internet access is off.
- A running chat/task still has stale authorization.

### `404 Not Found` for an existing repository

GitHub may return 404 when the caller is not authorized to see a repository through the selected installation. Also verify:

- Owner and repository spelling
- The correct GitHub account/organization installation
- Repository selection under **Only select repositories**

### Public repository can be read but not modified

This is expected when the repository is public but is not selected for the connector installation. Public repositories may be anonymously readable; authenticated write operations still require explicit repository access.

### Access works in one chat but not another

- Confirm the second chat has the GitHub connector available.
- Reload or recreate the second chat after changing the installation.
- Confirm it is using the intended Codex environment.
- Ask it to use the GitHub connector rather than relying solely on an unauthenticated shell request.

## Safe maintenance

- Prefer **Only select repositories** unless broad access is intentionally desired.
- Add new repositories when they are created.
- Remove repositories that no longer need connector access.
- Do not select **Suspend** or **Uninstall** while active projects depend on the connector.
- The installation URL/ID is not a credential, but never commit GitHub tokens, passwords, or private keys.

## Quick checklist for a new game repository

- [ ] Repository created under the intended GitHub owner
- [ ] ChatGPT Codex Connector installed
- [ ] Repository added under **Repository access**
- [ ] Changes saved in GitHub
- [ ] Connector/chat refreshed
- [ ] `README.md` fetch verified
- [ ] Intended write operation verified
- [ ] Codex environment selected
- [ ] Agent internet access enabled if shell networking is needed
- [ ] Environment cache reset if configuration changed
