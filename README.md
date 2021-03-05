# node-zap 
### Free Open Source Whatsapp Api

Este projeto usa como base o [Venom-bot](https://github.com/orkestral/venom), um navegador virtual sem interface gráfica que abre o whatsapp web e executa todos os comandos via código possibilitando assim a automação de todas as funções.

_OBS: está utilizando a versão 3.0.6 do venom-bot_

## Setup

- para instalar todas as dependencias necessárias no sistema

`curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`

`sudo apt install -y git nodejs yarn`
- para instalar git, nodejs

`git clone https://github.com/mauriciovilela/node-zap.git`

`cd node-zap`

`cp .env-example .env`

`npm install`

### Start server

`node index.js`

## Usage

### Start new whatsapp session

`http://localhost:3000/start?sessionName=session1`

### Ler QRCode no terminal

Após iniciar a sessão irá aparecer no terminal o QR CODE (Registre ele no seu whatsapp)

### Ler QRCode no browser

`http://localhost:3000/qrcode?sessionName=osdent&image=true`

### Send message (POST method)

```javascript
curl -L -X POST 'http://localhost:3000/sendText' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
--data-raw '{
    "sessionName": "session1", 
    "number": "553411112222",
    "text": "Teste"
}'
```

### Close whatsapp session

`http://localhost:3000/close?sessionName=session1`

## Salvar token do venom na nuvem (Opcional)

 - Crie uma conta grátis no https://jsonbin.io/ 
 - Crie um novo "bin" (objeto json) com quaisquer dados e copie o id dele e coloque no arquivo .env
 - Copie também o seu token de acesso à api do jsonbin.io e coloque no arquivo .env

```
...
JSONBINIO_BIN_ID=23452345345 <- aqui
JSONBINIO_SECRET_KEY=345234532452452345243 <- aqui
...
```

 - com esses dados o myzap irá gravar o token na nuvem e poderá ser executado em várias instancias diferentes por exemplo no Gooogle Cloud Run

### Manter os processos ativos a cada reinicialização do servidor 

`npm install -y pm2 -g`

`pm2 start index.js --name "node-zap" --max-memory-restart 120M`

`pm2 startup`

### Utilizar o docker (opcional)

`docker build -t node-zap .`

`docker run -ti -p 3000:3000 --name node-zap --restart=always note-zap`

