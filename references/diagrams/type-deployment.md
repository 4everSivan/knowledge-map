# Deployment

Show placement in hosts, environments and meaningful network scopes. State whether this is configuration-declared placement or an actual observed environment, including its source scope. Targets use separate target views.

## Semantic fields

Node roles: `host`, `workload`, `artifact`, `managed_service`. Optional node properties: `replicas` (nonnegative integer), `version` (string), `ports` (string array), only if supported. Relation kinds: `runs_on`, `deployed_to`, `connects_to`, `replicates_to`. Optional relation properties: `protocol` and `port` (strings). Group kinds: `environment`, `network_boundary`, `cluster`, `namespace`; supported nesting uses `parent_id`.

## Draw and check

Draw zones first, infrastructure and placed artifacts inside the correct scope. A logical database is not automatically a process inside a subnet. Show only placements and boundary paths established by evidence. Do not add a version, replica count or network port to complete a visual pattern. Keep unrelated environments separate or explicitly bounded. A manifest file proves desired configuration, not live pods, connectivity, failover or runtime replicas. Avoid real sensitive host details when unnecessary; never include credentials.
