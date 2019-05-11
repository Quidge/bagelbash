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

## 5/6

### Accomplished

- Not a lot. I have a much bettre idea about how the local networks can work with docker, though. I wasn't grabbing onto that before.
- I figured out how the `build` directive is used with `image`. Finally. That was confusing all of last week.
- Decided to stick the Orders local DB into its own container and store data in a `volume`.

### What I'm thinking about/todo next session:

- Setup a prisma server container and get it linked to the mysql container.

## 5/10

### Accomplished

- I was able to get the gql playground up inside a container, but it doesn't seem to be able to find the db server. No errors on stdout for the mysql db container. :/

### What I'm thinking about/todo next session:

- Do the prisma init cli and select a local docker db with mysql. Try that with docker-compose and see if the same issue pops up. I feel like I've done this before but I kinda feel out of options. Maybe post on Prisma Slack?

## 5/11

### Accomplished

- I got a Prisma server running! Except I've done that already; the difference was I get it working enough that GraphQL Playground could view and interact with the Schema.

### What I'm thinking about/todo next session:

- Based on my difficulty with the above, I don't think I have a good grounding in what `prisma deploy` is doing, and what Prisma "services" are. I need to research that.
