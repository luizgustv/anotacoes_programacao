FROM node:13-alpine

ENV ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    ME_CONFIG_MONGODB_ADMINPASSWORD=password

RUN mkdir -p /home/app

#copiando todos os arquivos da pasta /app para home/app (o dot se refere a todos os arquivos dentro da pasta)
COPY ./app /home/app

WORKDIR /home/app

RUN npm install

CMD ["node", "/home/app/server.js"]