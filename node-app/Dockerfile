FROM node:14-alpine

WORKDIR /usr/share/app

COPY . .

RUN npm install express morgan-body

EXPOSE 3000

CMD ["node", "app.js"]
