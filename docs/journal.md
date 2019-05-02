# dev log

So that I can keep track of what I was thinking about in my last session.

## 5/2:

### Accomplished:

- not a lot. gained a better understanding of how my dev env needs to look with docker.
- downloaded mysql. I decided to use AWS Aurora in prod. Aurora uses mysql, not postgres, so to will be rolling with mysql. nice part about Prisma is that i (theoretically) don't have to care about my db implementation.

### What I'm thinking about/todo next session:

- Dockerfile/docker-compose.yml setup. The whole project will have a docker-compose.yml file that will be used for local dev. during local dev, everything (except the db?) will be containerized and linked together. the purpose of this containerization is to replicate their prod independence.
  - i think local dev will run with `docker-compose up`
  - i think a push to prod will be an amalgem of `apex up`/`now .` + something that can deploy a docker container
- Prisma will have a Dockerfile that will set it's db connection to an env var which holds the dev/prod appropriate db location.
  - Prisma will end up on AWS Fargate or straight EC2
- i don't know yet if the frontend would need a Dockerfile. does every service need a dockerfile?
- this is what i'm thinking for the pieces:
  - Orders
    - DB
      - prod: AWS Aurora
      - local: localhost mysql
    - Prisma server
      - prod: Fargate/ec2 micro
      - local: container
  - apollo-yoga
    - prod: Apex/Now/some lambda
    - local: container
  - rest of the frontend
    - prod: Apex/Now/some lambda
    - local: container
  - Inventory (KISS version with a simple server taking no args that returns JSON)
    - prod: Apex/Now/some lambda
    - local: container
