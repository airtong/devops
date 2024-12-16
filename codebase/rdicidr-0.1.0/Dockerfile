# Fase 1: Builder - Instala dependências e compila o código
FROM node:15 as builder

# Definir o diretório de trabalho
WORKDIR /app

# Copiar os arquivos de dependência (package.json e package-lock.json)
COPY codebase/rdicidr-0.1.0/package*.json ./

# Instalar dependências
RUN npm install

# Copiar o código-fonte (src e public) para o contêiner
COPY codebase/rdicidr-0.1.0/ ./ 

# Executar o build da aplicação
RUN npm run build

# Fase 2: Final - Criar uma imagem leve com o código compilado
FROM node:15

# Definir o diretório de trabalho
WORKDIR /app

# Copiar os arquivos necessários do builder (build e package.json)
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./

# Instalar apenas as dependências de produção
RUN npm install --only=production

# Expor a porta 8080
EXPOSE 8080

# Definir o comando de entrada
ENTRYPOINT ["node", "dist/index.js"]
