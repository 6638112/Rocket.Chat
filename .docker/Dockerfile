FROM rocketchat/base:8

ENV RC_VERSION 0.60.0-develop

MAINTAINER buildmaster@rocket.chat

COPY Rocket.Chat.tar.gz ./

RUN set -x \
#  && curl -SLf "https://releases.rocket.chat/${RC_VERSION}/download/" -o rocket.chat.tgz \
#  && curl -SLf "https://releases.rocket.chat/${RC_VERSION}/asc" -o rocket.chat.tgz.asc \
#  && gpg --verify rocket.chat.tgz.asc \
 && mkdir -p /app \
 && tar -zxf Rocket.Chat.tar.gz -C /app \
 && rm Rocket.Chat.tar.gz \
 && cd /app/bundle/programs/server \
 && npm install \
 && npm cache clear --force \
 && chown -R rocketchat:rocketchat /app

USER rocketchat

VOLUME /app/uploads

WORKDIR /app/bundle

# needs a mongoinstance - defaults to container linking with alias 'mongo'
ENV DEPLOY_METHOD=docker \
    NODE_ENV=production \
    MONGO_URL=mongodb://wordpress-mongo.default.svc.cluster.local:27017/rocketchatdb \
    HOME=/tmp \
    PORT=3000 \
    ROOT_URL=http://chat.k12mlmq.com:3000 \
    Accounts_AvatarStorePath=/app/uploads

EXPOSE 3000

CMD ["node", "main.js"]
