# Server Ownership

Who's responsible for what servers?

## Production

Devops work with developers to make sure the servers provide the functionality required for our applications, but production servers and databases are ultimately the responsibility of the devops team.  Developers should not normally have direct access to a production server except under the supervision of a devop.  This is for your own protection.

Production servers comprise ec2 clusters of varying size for each application.

[links or embeds of system maps or lists?]

## Staging

The staging servers are the joint responsibility of the developers and devops.  They are managed via Chef by devops like production servers, but developers have direct access (root access when using `susan` user) to the servers for debugging purposes.

Most applications are spread across `staging14`, `staging15` and `staging16`.

[list of what apps are where?]

## Integration / CI

The build servers are the responsibility of devops.

[not sure what the layout of these servers is right now]

## Reporting

This is a MySQL replication server only `reporting1` and provides a real time replication server for running dev and cs queries against without affect the product database.

This database can be used for testing purposes against real-time production data (providing only read access is required) by modifying the revieworld `database.yml` file to point at `reporting1` (readonly username, no password)
