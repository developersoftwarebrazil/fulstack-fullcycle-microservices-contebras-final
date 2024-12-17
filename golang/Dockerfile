# Utilizando uma imagem oficial do Golang para desenvolvimento
FROM golang:1.23-alpine

# Instalação de ferramentas adicionais como git e ca-certificates
RUN apk add --no-cache git bash ffmpeg

# Definindo o diretório de trabalho dentro do container
WORKDIR /app

# Copiando o arquivo go.mod e go.sum para dentro do container
COPY go.mod go.sum ./

# Baixando as dependências
RUN go mod download

# Copiando o restante dos arquivos da aplicação para dentro do container
COPY . .

# Compilar a aplicação Go (pode ser modificado conforme o nome da sua aplicação)

# Definir o ponto de entrada (entrypoint) como bash para que você possa interagir
CMD [ "bash" "go", "run", "main.go"]




# Etapa 1: Build (compila o binário Go)
FROM golang:1.23-alpine AS builder

# Instalação de ferramentas adicionais necessárias
RUN apk add --no-cache git ffmpeg

# Definindo o diretório de trabalho
WORKDIR /app

# Copiando os arquivos necessários para dentro do container
COPY go.mod go.sum ./
RUN go mod download

# Copiando o restante do código
COPY . .

# Compilando o binário
RUN go build -o main .

# Etapa 2: Runtime (imagem final para execução)
FROM alpine:latest

# Instalação de dependências para execução
RUN apk add --no-cache ffmpeg

# Definindo o diretório de trabalho no container
WORKDIR /app

# Copiando o binário gerado na etapa de build
COPY --from=builder /app/main .

# Expondo a porta que o Railway usará para acessar sua aplicação
EXPOSE 8080

# Comando para iniciar a aplicação
CMD ["./main"]
