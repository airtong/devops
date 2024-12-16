# Fase 1: Builder - Instala dependências e compila o código
FROM node:15 as builder

# Definir o diretório de trabalho
WORKDIR /app

# Copiar package.json e package-lock.json para instalar dependências
COPY package*.json ./

# Instalar dependências
RUN npm install

# Copiar o restante do código da aplicação
COPY . .

# Executar o build da aplicação
RUN npm run build


# Fase 2: Final - Criar uma imagem leve com o código compilado
FROM node:15

# Definir o diretório de trabalho
WORKDIR /app

# Copiar apenas os arquivos necessários do builder
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./

# Instalar apenas as dependências de produção
RUN npm install --only=production

# Configurar a porta do container
EXPOSE 8080

# Definir o comando de entrada
ENTRYPOINT ["node", "dist/index.js"]
