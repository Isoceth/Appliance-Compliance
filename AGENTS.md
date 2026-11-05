# Appliance Compliance

Operate and diagnose the live Home Assistant instance from here — its
automations, configuration and devices — and publish the reusable artefacts
that come out of that work, such as the blueprints under `blueprints/`.

## Operating the live instance

Change the instance directly through its REST and websocket APIs or its
host shell, rather than handing the user YAML to paste in. The access details
are machine-local, in the uncommitted `CLAUDE.local.md`.

- Before changing an entity, automation or config, read its live state
  rather than relying on what this repository or an earlier session recorded.
- Change UI-managed configuration (automations, helpers, registries,
  dashboards) through the APIs. Core holds this state in memory and
  overwrites the files under `.storage/`, so a direct edit is lost or
  conflicts with the running instance.
- The house is lived in: switching lights, heating or plugs, and restarting
  core, take effect immediately. Act on what the task names; ask before a
  restart, an update, or switching devices the task did not mention.
- Take an HA backup before anything hard to undo — updates, firmware
  flashes, removing devices or bulk registry deletions.
- Verify the result on the instance: the state changed, the automation's
  trace ran the intended path, and the log shows no new errors. Run
  `ha core check` before restarting after YAML changes.

## Home Assistant documentation

Home Assistant's YAML schema and integrations change between releases, so
check the current documentation before writing or changing an automation,
blueprint or configuration entry — the Context7 Home Assistant feed when
Context7 is connected, home-assistant.io otherwise. Target the version the
instance runs (`GET /api/config` reports it), not the version you remember.

## Blueprints

A blueprint in this repository and the copy the instance runs are separate
files: the instance keeps its own under `blueprints/automation/Isoceth/` in
its config directory, whatever folder holds it here
(`circadian/circadian_room.yaml` here is `Isoceth/circadian_room.yaml`
there). Install or update the live copy with the websocket `blueprint/save`
command, passing this repository's raw GitHub URL as `source_url` so the
instance can re-import it. After changing a blueprint the
instance uses, update the live copy and call the `automation.reload`
service, then confirm the automations built on it are not `unavailable` and
the log shows no blueprint errors.

## What goes into Git

This repository is public, and pushed history is permanent. Commit only
what is safe to publish: blueprints and other reusable, instance-neutral
artefacts. Tokens, addresses, hostnames, device and entity names from the
house, live configuration dumps, backups and logs stay out of the
repository; keep working files from live sessions outside it.
