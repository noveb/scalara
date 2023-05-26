# scalara
Solution for the Scalara dev challange

---
## Prerequisites for development

* [Docker](https://www.docker.com/products/docker-desktop) and [docker-compose](https://docs.docker.com/compose/)
* [NodeJS](https://nodejs.org/en/) and [npm](https://www.npmjs.com/)

## Start locally for development

1. Clone the repo

    ```bash
    git clone https://github.com/noveb/scalara.git
    ```

2. Install development dependencies

    Most things can be done in/with Docker but it is still useful to install the dependencies. 
    
    ```bash
    npm ci
    ```

3. Copy template.env to .env

    ```bash
    cp template.env .env
    ```

4. Build Docker image for development

    ```bash
    docker-compose build
    ```

5. Run the Docker container for development

    ```bash
    docker-compose up
    ```

---

## Push image

```
docker build --target production -t scalara:latest .
```

```sh
docker tag $image_id $AWS_ACCOUNT_ID.dkr.ecr.eu-central-1.amazonaws.com/scalara:latest
```

```sh
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.eu-central-1.amazonaws.com
```

```sh
docker push $AWS_ACCOUNT_ID.dkr.ecr.eu-central-1.amazonaws.com/scalara:latest
```

## Add secrets and env vars to AWS Parameter Store

```
aws ssm put-parameter --name "....." --type "String" --value "....."
```