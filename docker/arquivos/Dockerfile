FROM node:13-alpine

ENV ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    ME_CONFIG_MONGODB_ADMINPASSWORD=password

RUN mkdir -p /home/app

# copia todos arquivos/diretório do host para sua imagem. Então foi copiado os arquivos da pasta /app (server.js) e /home/app
COPY ./app /home/app

# set default dir so that next commands executes in /home/app dir
WORKDIR /home/app

RUN npm install

CMD ["node", "server.js"]