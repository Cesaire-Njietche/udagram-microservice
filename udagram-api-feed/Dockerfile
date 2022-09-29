FROM node:13
# Créer le répertoire de l'application
WORKDIR /usr/src/app
# Installer les dépendances de l'application
# Un joker est utilisé pour s'assurer que le paquet.json ET le paquet-lock.json sont copiés lorsqu'ils sont disponibles (npm@5+)
COPY package*.json ./
#Install aws cli
RUN apt-get update && apt-get install -y python python-dev python-pip python-setuptools \
    && pip install awscli && apt-get clean

# args
ARG AWS_KEY=AKIA3DIVAY4WCXEXEBZK
ARG AWS_SECRET=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
ARG AWS_REGION=us-east-1

RUN aws configure set aws_access_key_id $AWS_KEY
RUN aws configure set aws_secret_access_key $AWS_SECRET
RUN aws configure set default.region $AWS_REGION
RUN npm ci
# Regroupement des sources de l'application
COPY . .
EXPOSE 8080
CMD [ "npm", "run", "prod" ]