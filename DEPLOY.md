## Install HTMLCOIN API

1. install mongodb https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/
2. install htmlcoin-bitcore daemon -b master-bitcore https://github.com/HTMLCOIN/htmlcoin.git
3. vim ~/.htmlcoin/htmlcoin.conf
```
server=1
whitelist=127.0.0.1
txindex=1
addressindex=1
timestampindex=1
spentindex=1
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
rpcallowip=127.0.0.1
rpcuser=htmlcoin
rpcpassword=htmlcoinpassword
rpcport=18332
reindex=1
gen=0
addrindex=1
rpcworkqueue=300
logevents=1
maxconnections=500
```
## INSTALL SERVER-RECEIVE

4. git clone https://github.com/denuoweb/server-api-receive
5. cd server-receive
6. npm install
7. cp config/main.json.bak config/main.json
8. vim config/main.json
```
{ 
    "PORT":5555,
    "ZMQ_URL":"tcp://127.0.0.1:28332",
    "NETWORK":"testnet",
    "SIGNATURE_LIFETIME_SEC":5,
    "UPDATE_FROM_BLOCK_HEIGHT": 100000,
    "ENCRYPT_PRIVATE_KEY_SALT":"!super_sE_c_R_eT_SaLt_super!",
    "RPC":{ 
        "PROTOCOL":"http",
        "HOST":"127.0.0.1",
        "PORT":"18332",
        "USER":"htmlcoin",
        "PASSWORD":"htmlcoinpassword"
    },
    "db":{ 
        "host":"127.0.0.1",
        "port":"27017",
        "database":"server_receive"
    }
}
```

9. Create account with server-receive API:

`POST http://localhost:5555/api/v1/users`

Request Example:

{
"password": "5ba8a72c63a7c8303cdfbfec",
"email": "testemail@email.com"
}

https://i.imgur.com/LoTcCCL.png

10. Create keys

POST http://localhost:5555/api/v1/keys

https://i.imgur.com/5NjrP84.png

11. npm run start
12. api endpoint is http://127.0.0.1:5555/api

## INSTALL MOBILE-API-SERVER

13. git clone https://github.com/denuoweb/mobile-api-server.git
14. cd mobile-api-server
15. Select a branch: git checkout development || stage || master
16. npm install
17. cp config/main.json.bak config/main.json
18. vim config/main.json
```
{
    "ENVIRONMENT": "DEV",
    "INSIGHT_API_SOCKET_SERVER": "http://127.0.0.1:3001",
    "INSIGHT_API_URL": "http://127.0.0.1:3001/insight-api",
    "NETWORK": "testnet",
    "DB": {
        "HOST": "127.0.0.1",
        "PORT": "27017",
        "DATABASE": "server",
        "USER": "",
        "PASSWORD": ""
    },
    "FIREBASE_SERVER_TOKEN": "--FIREBASE-SERVER-TOKEN--",
    "disableRaven": "1",
    "RECEIVE_API": {
        "URL": "http://127.0.0.1:5555",
        "PRIVATE_KEY": "--PRIVATE KEY FROM SERVER RECEIVE--",
        "PUBLIC_KEY": "--PUBLIC KEY FROM SERVER RECEIVE--"
    }
}
```
19. npm run start
20. api endpoint is http://127.0.0.1:5931/api
