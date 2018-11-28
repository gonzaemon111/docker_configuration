FROM node:10-alpine
ENV LANG C.UTF-8

RUN mkdir ./practice_frontend

COPY . /practice_frontend
WORKDIR /practice_frontend

# Set environment variables
ENV NODE_ENV development
ENV HOST 0.0.0.0
EXPOSE 3000
# Bundle app source
RUN yarn global add vue-cli
RUN yarn install

CMD ["yarn", "dev"]
