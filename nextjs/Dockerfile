# Usar uma imagem leve do Node.js
FROM node:22.8.0-slim

# Configura variáveis de ambiente para otimizar o ambiente de produção
ENV NODE_ENV production

# Define o usuário padrão como `node` (não-root)
USER node

# Define o diretório de trabalho no container
WORKDIR /home/node/app

# Copia os arquivos de dependência do projeto (package.json e package-lock.json)
COPY --chown=node:node package.json package-lock.json ./

# Instala apenas as dependências de produção
RUN npm install --omit=dev

# Copia o restante dos arquivos do projeto para o container
COPY --chown=node:node . .

# Compila a aplicação para produção
RUN npm run build

# Expõe a porta padrão do Next.js (Railway redirecionará a porta automaticamente)
EXPOSE 3000

# Define o comando para iniciar a aplicação Next.js
CMD ["npm", "run", "start"]




# FROM node:22.8.0-slim 

# USER node

# WORKDIR /home/node/app

# CMD ["tail", "-f", "/dev/null"]