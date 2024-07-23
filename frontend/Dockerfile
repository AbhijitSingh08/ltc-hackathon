FROM node:14 AS build-stage

WORKDIR /frontend

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

RUN ls -la /frontend/dist

FROM node:14

WORKDIR /frontend

COPY --from=build-stage /frontend/dist /frontend/dist

RUN npm install -g serve

EXPOSE 80

CMD ["serve", "-s", "dist", "-l", "80"]