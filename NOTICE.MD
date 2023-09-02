1. Setup AWS: Add a PostgreSQL database in RDS
Endpoint (Hostname): database-1.ch4a9dhlinpw.us-east-1.rds.amazonaws.com 
Instance identifier: database-1 //This is not the database name
Database name: postgres (default)
Username: postgres
Password: mypassword
Port: 5432

1. For Circle CI: Set env for Circle CI project
AWS_ACCESS_KEY_ID=(from IAM user with programmatic access)
AWS_SECRET_ACCESS_KEY= (from IAM user with programmatic access)
AWS_DEFAULT_REGION=(your default region in aws)
TYPEORM_CONNECTION=postgres
TYPEORM_MIGRATIONS_DIR=./src/migrations
TYPEORM_ENTITIES=./src/modules/domain/**/*.entity.ts
TYPEORM_MIGRATIONS=./src/migrations/*.ts
TYPEORM_HOST={your postgres database hostname in RDS}
TYPEORM_PORT=5432 (or the port from RDS if it’s different)
TYPEORM_USERNAME={your postgres database username in RDS}
TYPEORM_PASSWORD={your postgres database password in RDS}
TYPEORM_DATABASE=postgres {or your postgres database name in RDS}

1. Jobs list
workflows:
  default:
    jobs:
      - build-frontend
      - build-backend
      - test-frontend:
          requires: [build-frontend]
      - test-backend:
          requires: [build-backend]
      - scan-backend:
          requires: [build-backend]
      - scan-frontend:
          requires: [build-frontend]
      - deploy-infrastructure:
          requires: [test-frontend, test-backend, scan-frontend, scan-backend]
          filters:
            branches:
              only: [test-feature-branch]
      - configure-infrastructure:
          requires: [deploy-infrastructure]
      - run-migrations:
          requires: [configure-infrastructure]
      - deploy-frontend:
          requires: [run-migrations]
      - deploy-backend:
          requires: [run-migrations]
      - smoke-test:
          requires: [deploy-backend, deploy-frontend]
      - cloudfront-update:
          requires: [smoke-test]
      - cleanup:
          requires: [cloudfront-update]
