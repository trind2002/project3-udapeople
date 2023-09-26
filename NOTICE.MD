1. Setup AWS: Add a PostgreSQL database in RDS
Endpoint (Hostname): database-1.ch4a9dhlinpw.us-east-1.rds.amazonaws.com 
Instance identifier: database-1 //This is not the database name
Database name: postgres (default)
Username: postgres
Password: mypassword
Port: 5432

1. For Circle CI: Set env for Circle CI project
AWS_ACCESS_KEY_ID=ASIAWGFXITUAXMLKVXE6
AWS_SECRET_ACCESS_KEY=enlMSTfF51q+1hxLlj18E+x6ZdB/ckrZx9W/SosA
AWS_DEFAULT_REGION=us-east-1
AWS_SESSION_TOKEN=
TYPEORM_CONNECTION=postgres
TYPEORM_MIGRATIONS_DIR=./src/migrations
TYPEORM_ENTITIES=./src/modules/domain/**/*.entity.ts
TYPEORM_MIGRATIONS=./src/migrations/*.ts
TYPEORM_HOST={your postgres database hostname in RDS}
TYPEORM_PORT=5432 (or the port from RDS if it’s different)
TYPEORM_USERNAME={your postgres database username in RDS}
TYPEORM_PASSWORD={your postgres database password in RDS}
TYPEORM_DATABASE=postgres {or your postgres database name in RDS}

Building a Continuous Integration Pipeline
Sharing Information
# Syntax
curl -d 'email=trind7.register@gmail.com' https://kvdb.io -> GnKyNnpF737L7n1W7dcs5G 
# Returns a bucket ID, such as, "XsgrYuyPESbxCcte4sLxEM"

# Syntax
curl https://kvdb.io/[bucket-ID]/[key]  -d '[value]'
# Example
curl https://kvdb.io/GnKyNnpF737L7n1W7dcs5G/migration_$\{CIRCLE_WORKFLOW_ID:0:7\}  -d '1'

# Syntax
curl --insecure  https://kvdb.io/[bucket-ID]/[key]
# Example
curl --insecure  https://kvdb.io/4rFJyH4hNUAdKbwRLrY43L/migration_$\{CIRCLE_WORKFLOW_ID:0:7\}
# Trigger Cleanup

Prometheus: Intsall 
https://codewizardly.com/prometheus-on-aws-ec2-part1/

alert rule file
groups:
- name: alert.rules
  rules:
  - alert: InstanceDown
    expr: up == 0
    for: 1m
    labels:
      severity: "critical"
    annotations:
      summary: "Endpoint {{ $labels.instance }} down"
      description: "{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 1 minutes."