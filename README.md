# MyZap - Free Open Source Whatsapp Api

Este projeto usa como base o [Venom-bot](https://github.com/orkestral/venom), um navegador virtual sem interface gráfica que abre o whatsapp web e executa todos os comandos via código possibilitando assim a automação de todas as funções.

## Setup

- para instalar todas as dependencias necessárias no sistema

`curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`

`sudo apt install -y git nodejs`
- para instalar git, nodejs

`git clone https://github.com/billbarsch/myzap.git`

`cd myzap`

`npm install`

`cp .env-example .env`

### Start server

`node index.js`

### keep processes alive at every server restart

`npm install -y pm2 -g`

`pm2 start index.js`

`pm2 startup`

## Usage

### Start new whatsapp session

`http://localhost:3333/start?sessionName=session1`

### Get QRCode on terminal


### Send message (POST method)

```javascript
(async () => {
  const response = await fetch('http://localhost:3333/sendText', {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(
        {
            sessionName: "session1", 
            number: '556334140378',
            text:"Hello\nWorld"
        }
    )
  });
  const content = await response.json();

  console.log(content);
})();  
```

### Send File (POST method)

```javascript
curl -L -X POST 'http://localhost:3333/sendText' \
-H 'Accept: application/json' \
-H 'Content-Type: application/json' \
--data-raw '{
    "sessionName": "session1", 
    "number": "553411112222",
    "text": "Teste"
}'
```

### Close whatsapp session

`http://localhost:3333/close?sessionName=session1`

## Salvar token do venom na nuvem
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
