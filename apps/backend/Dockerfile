FROM node:20-alpine
RUN corepack enable && corepack prepare pnpm@9.15.0 --activate

WORKDIR /app

COPY package.json ./
RUN printf "auto-install-peers=true\nstrict-peer-dependencies=false\nshamefully-hoist=true\nengine-strict=true\n" > .npmrc
RUN pnpm install --no-frozen-lockfile

COPY . .
RUN pnpm build

EXPOSE 9000
CMD ["sh", "-c", "node_modules/.bin/medusa db:migrate && node_modules/.bin/medusa start"]
