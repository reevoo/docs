# Server Ownership

Who's responsible for what servers?

## Production

Devops work with developers to make sure the servers provide the functionality required for our applications, but production servers and databases are ultimately the responsibility of the devops team.  Developers should not normally have direct access to a production server except under the supervision of a devop.  This is for your own protection.

Production servers comprise ec2 clusters of varying size for each application.

[links or embeds of system maps or lists?]

## Staging

The staging servers are the joint responsibility of the developers and devops.  They are managed via Chef by devops like production servers, but developers have direct access (but not root access) to the servers for debugging purposes.

Most applications are spread across `staging5` and `staging6`.

[list of what apps are where?]

## Integration / CI

The build servers are the sole responsibility of the developers.  The devops will assist when requested.

[not sure what the layout of these servers is right now]

## R&D

The R&D servers and databases are the joint responsibility of the Head of R&D and the devops.  They are managed via Chef by devops like production servers, but the Head of R&D has direct access (including root access) to the servers for administration purposes.

These comprise:

- An EU cluster of servers named `tr1` and `tr2` acting as:
  * "Bunnyhop" R&D tracking endpoints.
  * Web hosts for various small R&D applications.
- A US server named `tracking-io` acting as a sorting house for track events passed from `tr1` and `tr2`.
- A large EBS drive attached to `tracking-io` holding historical track events as JSON.
- A PaaS called Treasure Data holding a queryable copy of our historical track events.
- A number of application server replicas kept dormant when not running experiments.
- An R&D database connected via SSL to various short-lived Heroku applications.

## Reporting

This is a MySQL replication server only `reporting6` and provides a real time replication server for running dev and cs queries against without affect the product database.

This database can be used for testing purposes against real-time production data (providing only read access is required) by modifying the revieworld `database.yml` file to point at `reporting6` with the appropriate password (see dev team for password)
