# API

All endpoints only accept POST requests with a JSON body.

## findIntents

---

- **URL**

  `/findIntents`

- **Data Params**

  ```js
    {
    "makerTokens": Array<string>,
    "takerTokens": Array<string>
    }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
  http://localhost:5005/findIntents \
  -H 'Content-Type: application/json' \
  -d '{
    "makerTokens": ["0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8"],
    "takerTokens": ["0x0000000000000000000000000000000000000000"]
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  [{
    "address": "0x6cc47be912a07fbe9cebe68c9e103fdf123b7269",
    "makerToken": 0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8,
    "takerToken": 0x0000000000000000000000000000000000000000,
    "role": "maker"
  },
  ...]
  ```

## setIntents

---

- **URL**

  `/setIntents`

- **Data Params**

  ```json
  [{
    "makerToken": string,
    "takerToken": string,
    "role": string
  },
  ...]
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/setIntents \
    -H 'Content-Type: application/json' \
    -d '[{
    "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
    "takerToken": "0x0000000000000000000000000000000000000000",
    "role": "maker"
  }]'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:** `ok`

## getIntents

---

- **URL**

  `/getIntents`

- **Data Params**

  ```json
  {
    "address": string
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/getIntents \
    -H 'Content-Type: application/json' \
    -d '{
    "address": "0x6cc47be912a07fbe9cebe68c9e103fdf123b7269"
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  [
    {
      "address": "0x2369267687a84ac7b494dae2f1542c40e37f4455",
      "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
      "takerToken": "0x0000000000000000000000000000000000000000",
      "role": "maker"
    }
  ]
  ```

- **Notes:**
  The address specified in Data Params is case sensitive.

## getOrder

---

- **URL**

  `/getOrder`

- **Data Params**

  ```js
  {
    "makerAddress": string,
    "params":
    {
      "makerAmount": string,
      "makerToken": string,
      "takerToken": string
    }
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/getOrder \
    -H 'Content-Type: application/json' \
    -d '  {
      "makerAddress": "0x6cc47be912a07fbe9cebe68c9e103fdf123b7269",
      "params": {
        "makerAmount": "100000",
        "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
        "takerToken": "0x0000000000000000000000000000000000000000"
      }
    }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "makerAddress": "0x6cc47be912a07fbe9cebe68c9e103fdf123b7269",
    "makerAmount": "100000",
    "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
    "takerAddress": "0x61ba956bb7d4e7146efaf74ccf327d213e96713c",
    "takerAmount": "2993000000000000",
    "takerToken": "0x0000000000000000000000000000000000000000",
    "expiration": 1532447264,
    "nonce": "33382012",
    "v": 27,
    "r": "0xd0382d77c3adf0641f05f64a49cf5011a0324129fddf961dfc7c98732e58a42e",
    "s": "0x3f671cbd665786459b516f3ae054aa6742e049449c8271a3f5c44e8c1925e4d0"
  }
  ```

## getQuote

---

- **URL**

  `/getQuote`

- **Data Params**

  ```js
  {
      "makerAddress": string,
      "makerToken": string,
      "takerToken": string,
      "makerAmount"?: string,
      "takerAmount"?: string,
  }
  ```

- **Sample Call:**

  ```bash
    curl -X POST \
      http://localhost:5005/getQuote \
      -H 'Cache-Control: no-cache' \
      -H 'Content-Type: application/json' \
      -H 'Postman-Token: 4fc1a07a-0fde-457c-a3d4-9288a529004f' \
      -d '{
    "makerAddress": "0x1550d41be3651686e1aeeea073d8d403d0bd2e30",
    "makerToken": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
    "takerToken": "0x0000000000000000000000000000000000000000",
    "makerAmount": "100000000000000000000"
    }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "makerAddress": "0x1550d41be3651686e1aeeea073d8d403d0bd2e30",
    "makerAmount": "100000000000000000000",
    "makerToken": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
    "takerAmount": "394652714438327229",
    "takerToken": "0x0000000000000000000000000000000000000000"
  }
  ```

- **Notes:**
  You should only specify one of EITHER makerAmount OR takerAmount in the data params. The maker who is providing the quote will fill in the other side in their response.

## getMaxQuote

---

- **URL**

  `/getMaxQuote`

- **Data Params**

  ```js
  {
    "makerAddress": string,
    "makerToken": string,
    "takerToken": string,
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
  http://localhost:5005/getMaxQuote \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 7237a3bf-4cf6-494b-9792-02c703333173' \
  -d '{
  "makerAddress": "0x1550d41be3651686e1aeeea073d8d403d0bd2e30",
  "makerToken": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
  "takerToken": "0x0000000000000000000000000000000000000000"
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "makerAddress": "0x1550d41be3651686e1aeeea073d8d403d0bd2e30",
    "makerAmount": "160620564837625881613380",
    "makerToken": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
    "takerAmount": "634403212441595956115",
    "takerToken": "0x0000000000000000000000000000000000000000"
  }
  ```

## signOrder

---

- **URL**

  `/signOrder`

- **Data Params**

  ```js
  {
    makerAddress: string,
    makerAmount: string,
    makerToken: string,
    takerAddress: string,
    takerAmount: string,
    takerToken: string,
    expiration: number,
    nonce: string
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/signOrder \
    -H 'Content-Type: application/json' \
    -d '    {
    "makerAddress": "0x6cc47be912a07fbe9cebe68c9e103fdf123b7269",
    "makerAmount": "100000",
    "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
    "takerAddress": "0x61ba956bb7d4e7146efaf74ccf327d213e96713c",
    "takerAmount": "2993000000000000",
    "takerToken": "0x0000000000000000000000000000000000000000",
    "expiration": 1532447264,
    "nonce": "33382012"
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "makerAddress": "0x6cc47be912a07fbe9cebe68c9e103fdf123b7269",
    "makerAmount": "100000",
    "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
    "takerAddress": "0x61ba956bb7d4e7146efaf74ccf327d213e96713c",
    "takerAmount": "2993000000000000",
    "takerToken": "0x0000000000000000000000000000000000000000",
    "expiration": 1532447264,
    "nonce": "33382012",
    "v": 27,
    "r": "0xd0382d77c3adf0641f05f64a49cf5011a0324129fddf961dfc7c98732e58a42e",
    "s": "0x3f671cbd665786459b516f3ae054aa6742e049449c8271a3f5c44e8c1925e4d0"
  }
  ```

## fillOrder

---

- **URL**

  `/fillOrder`

- **Data Params**

  ```js
  {
    "order": {
        "makerAddress": "0x60834d72a52B0Ddc1601f7739f44632CCfbf3886",
        "makerAmount": "10000",
        "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
        "takerAddress": "0x61ba956bb7d4e7146efaf74ccf327d213e96713c",
        "takerAmount": "1000000000000000",
        "takerToken": "0x0000000000000000000000000000000000000000",
        "expiration": 1532452110,
        "nonce": "6466",
        "r": "0xab65c90919c2bbb31764dcc450a9d4fffbabddf8363b7b1dc5a0ef2235274635",
        "s": "0x3d099c0af5f1ecc2ccf7999160d6d62f3c1fc16c66749a527962b804e990aefb",
        "v": 27
    },
    "config": {
      value: string,
      gasLimit: number,
      gasPrice: string
    }
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/fillOrder \
    -H 'Content-Type: application/json' \
    -d '{
    "order": {
        "makerAddress": "0x60834d72a52B0Ddc1601f7739f44632CCfbf3886",
        "makerAmount": "10000",
        "makerToken": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
        "takerAddress": "0x61ba956bb7d4e7146efaf74ccf327d213e96713c",
        "takerAmount": "1000000000000000",
        "takerToken": "0x0000000000000000000000000000000000000000",
        "expiration": 1532452110,
        "nonce": "6466",
        "r": "0xab65c90919c2bbb31764dcc450a9d4fffbabddf8363b7b1dc5a0ef2235274635",
        "s": "0x3d099c0af5f1ecc2ccf7999160d6d62f3c1fc16c66749a527962b804e990aefb",
        "v": 27
    },
    "config": {}
  }'
  ```

- **Notes:**
  The `config` key in data params is optional

- **Sample Response:**

  - **Code:** 200
  - **Content:**

  ```json
  {
    "nonce": 20,
    "gasPrice": {
      "_bn": "9502f9000"
    },
    "gasLimit": {
      "_bn": "27100"
    },
    "to": "0x07fC7c43D8168a2730344E5CF958aaecc3B42B41",
    "value": {
      "_bn": "0"
    },
    "data": "0x1d4d691d00000000000000000000000060834d72a52b0ddc1601f7739f44632ccfbf38860000000000000000000000000000000000000000000000000000000000002710000000000000000000000000cc1cbd4f67cceb7c001bd4adf98451237a193ff800000000000000000000000061ba956bb7d4e7146efaf74ccf327d213e96713c00000000000000000000000000000000000000000000000000038d7ea4c680000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000005b575d0e0000000000000000000000000000000000000000000000000000000000001942000000000000000000000000000000000000000000000000000000000000001bab65c90919c2bbb31764dcc450a9d4fffbabddf8363b7b1dc5a0ef22352746353d099c0af5f1ecc2ccf7999160d6d62f3c1fc16c66749a527962b804e990aefb",
    "v": 43,
    "r": "0x87288ad9ac4b15fed159857cb30a46c6ddb52f48cae1fb05820732596dcf27ca",
    "s": "0x68a284764d3b97093ad0196cc68abc8fce676f41e2484ac5a1762a372527f390",
    "chainId": 4,
    "from": "0x61ba956Bb7D4e7146eFaf74Ccf327d213e96713C",
    "hash": "0x9bac349471a0553abb9aa146ca68296c1987a57cdc8e1062be73fed95194aaf4"
  }
  ```
## wrap WETH

---

- **URL**

  `/wrapWeth`

- **Data Params**

  ```js
  {
    "amount": string,
    "config": {
      value: string,
      gasLimit: number,
      gasPrice: string
    }
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/wrapWeth \
    -H 'Content-Type: application/json' \
    -d '{
    "amount": "10000000000000000",
    "config": {}
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "nonce": 21,
    "gasPrice": {
        "_bn": "9502f9000"
    },
    "gasLimit": {
        "_bn": "27100"
    },
    "to": "0xc778417E063141139Fce010982780140Aa0cD5Ab",
    "value": {
        "_bn": "0"
    },
    "data": "0x2e1a7d4d000000000000000000000000000000000001ed09bead87c0378d8e6400000000",
    "v": 44,
    "r": "0x0bb55004cb08e6834881b64a503295a6030b8aab19806810ae9608c84aa7b2e9",
    "s": "0x11e1094c6e00093577dacd433a752687c384f1c92f86a45e2992633046f9e1e7",
    "chainId": 4,
    "from": "0x61ba956Bb7D4e7146eFaf74Ccf327d213e96713C",
    "hash": "0xb4de23394c51ca871e64f77ef3d7ac81f57fe93e58e87bc62cebb0c84da19e98"
  }
  ```

- **Notes:**
  `amount` must be denominated in WEI. The `config` key in data params is optional.


## unwrapWeth

---

- **URL**

  `/unwrapWeth`

- **Data Params**

  ```js
  {
    "amount": string,
    "config": {
      value: string,
      gasLimit: number,
      gasPrice: string
    }
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/unwrapWeth \
    -H 'Content-Type: application/json' \
    -d '{
    "amount": "10000000000000000",
    "config": {}
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "nonce": 21,
    "gasPrice": {
      "_bn": "9502f9000"
    },
    "gasLimit": {
      "_bn": "27100"
    },
    "to": "0xc778417E063141139Fce010982780140Aa0cD5Ab",
    "value": {
      "_bn": "0"
    },
    "data": "0x2e1a7d4d000000000000000000000000000000000001ed09bead87c0378d8e6400000000",
    "v": 44,
    "r": "0x0bb55004cb08e6834881b64a503295a6030b8aab19806810ae9608c84aa7b2e9",
    "s": "0x11e1094c6e00093577dacd433a752687c384f1c92f86a45e2992633046f9e1e7",
    "chainId": 4,
    "from": "0x61ba956Bb7D4e7146eFaf74Ccf327d213e96713C",
    "hash": "0xb4de23394c51ca871e64f77ef3d7ac81f57fe93e58e87bc62cebb0c84da19e98"
  }
  ```

- **Notes:**
  `amount` must be denominated in WEI. The `config` key in data params is optional.

## approveTokenForTrade

---

- **URL**

  `/approveTokenForTrade`

- **Data Params**

  ```js
  {
    "tokenContractAddr": string,
    "config": {
      value: string,
      gasLimit: number,
      gasPrice: string
    }
  }
  ```

- **Sample Call:**

  ```bash
  curl -X POST \
    http://localhost:5005/approveTokenForTrade \
    -H 'Content-Type: application/json' \
    -d '{
    "tokenContractAddr": "0xcc1cbd4f67cceb7c001bd4adf98451237a193ff8",
    "config": {}
  }'
  ```

- **Sample Response:**

  - **Code:** 200 <br />
  - **Content:**

  ```json
  {
    "nonce": 23,
    "gasPrice": {
      "_bn": "9502f9000"
    },
    "gasLimit": {
      "_bn": "27100"
    },
    "to": "0xCC1CBD4f67cCeb7c001bD4aDF98451237a193Ff8",
    "value": {
      "_bn": "0"
    },
    "data": "0x095ea7b300000000000000000000000007fc7c43d8168a2730344e5cf958aaecc3b42b410000000000000000000000000000000000000000033b2e3c9fd0803ce8000000",
    "v": 43,
    "r": "0x4ce519845525c54da7a71504ece39d5d82740be16f0c9ec72376779ea889cee4",
    "s": "0x532a8313693309f03727fbd3b80280c3ed7f2baa59abdeeb69d722b882f2a795",
    "chainId": 4,
    "from": "0x61ba956Bb7D4e7146eFaf74Ccf327d213e96713C",
    "hash": "0xfaa790499265fb27b90fcfc25563c5a640d7e2df417076e75e437a04ac325d00"
  }
  ```

- **Notes:**
  The `config` key in data params is optional.

## registerPGPKey

---

- **URL**

`/registerPGPKey`

- **Sample Call:**

```bash
curl -X POST \
  http://localhost:5005/registerPGPKey
```

- **Sample Response:**

- **Code:** 200 <br />
- **Content:**

```json
{
  "nonce": 150,
  "gasPrice": {
    "_bn": "9502f9000"
  },
  "gasLimit": {
    "_bn": "27100"
  },
  "to": "0x9D7eFd45E45C575CafB25d49d43556f43EbE3456",
  "value": {
    "_bn": "0"
  },
  "data": "0xce09197e000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000317a62327268646a44736f5566646867757a4c735a3866426455504257364e78326a714c39334e565a594635547553677637000000000000000000000000000000",
  "v": 43,
  "r": "0x2c0370b3dde7e1bb6eff58095e00f7c671c82d465e713c133746fe0987f32efa",
  "s": "0x6fcd36be59d3beeea4d9340633b3f371e39e161b84539be3c397e066c1601f1a",
  "chainId": 4,
  "from": "0xDead0717B16b9F56EB6e308E4b29230dc0eEE0B6",
  "hash": "0x78b6fe986c550e878b32a02dd50e3376c02998eddfbea60c1ae933378a888e3"
}
```
