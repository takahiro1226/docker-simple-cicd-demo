FROM node:18 AS base

CMD [ "bash" ]

# Build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
# docker-compose.ymlで指定した値　github actionで使う npm run buildでjavascriptをインストールするとき使う
RUN npm ci && mpm run test && npm run build

# Hosting in nginx
# このステージが実行されるときには、test-and-buildステージが実行されている
FROM nginx:latest AS production
COPY --from=test-and-build /workspace/build /var/www
COPY nginx.conf /etc/nginx/conf.d/default.conf