### RPC INFO

#### URL
```
'https://api.trongrid.io'
```
#### DEMO

there is the dev docs for tron network,use this api to get the bolock info:

https://developers.tron.network/reference/getblock-1

e.g:

```
request:

$.post('https://api.trongrid.io/wallet/getblockbynum', {"num" : 100}, function(data) {
    console.log(data);
});

response:

{
  "blockID": "00000000000f424013e51b18e0782a32fa079ddafdb2f4c343468cf8896dc887",
  "block_header": {
    "raw_data": {
      "number": 1000000,
      "txTrieRoot": "e2dd42daa9c853e070df1e4fc927851a7438c601fb12cf945922629d5cec187b",
      "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
      "parentHash": "00000000000f423fbccd9cdb9e410eabdf9f94145cf5b71a678b8b9616619125",
      "version": 9,
      "timestamp": 1578594852000
    },
    "witness_signature": "179caed28b3d129dee6d553ae6761a8c8698f890e5f38e062d56e2d0d0b8c9a20317b7753b3fd1be261935d6182434a6c057f8926f25027b9859cde3da3a655300"
  }
}
```