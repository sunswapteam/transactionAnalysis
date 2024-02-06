## 相关合约：

### sunswap V2

#### router

TKzxdSv2FZKQrEqkKVgp5DcwEXBEKMg2Ax

ABI 见 V2Router.abi

#### factory

TKWJdrQkqHisa1X8HUdHEfREvTzw4pMAaY
ABI 见 V2Factory.abi


#### Pair

地址 ：
router.getPairOffChain(tokenA,tokenB)
或 factory.getPair(tokenA,tokenB)

ABI 见 V2Pair.abi

### sunswap V3

#### factory

TThJt8zaJzJMhCEScH7zWKnp5buVZqys9x

ABI 见 V3Factory.abi
#### router

TQAvWQpT9H916GckwWDJNhYZvQMkuRL7PN

ABI 见 V3SwapRouter.abi

#### nftpostionmanager

TLSWrv7eC1AZCXkRjpqMZUmvgd99cj7pPF

ABI 见 V3NFTPostionManager.abi


#### pool

获取池子地址：

factory.getPool(tokenA,tokenB,费率);

当前费率： 100、500、3000、10000 对应四个等级的交易池
获取池子的

### 智能路由合约

TFVisXFaijZfeyeSjCEVkHfex7HGdTxzF9

ABI 见 SmartExchangeRouter.abi

### curveswap

地址：

Old 2pool(USDD+USDT) TAUGwRhmCP518Bm4VBqv7hDun9fg8kYjC4

2pool(TUSD+USDT) TS8d3ZrSxiGZkqhJqMzFKHEC1pjaowFMBJ

USDC Pool(USDC+TUSD+USDT) TE7SB1v9vRbYRe5aJMWQWp9yfE2k9hnn3s

USDJ Pool(USDJ+TUSD+USDT) TKBqNLyGJRQbpuMhaT49qG7adcxxmFaVxd

Usdd pool(USDD+TUSD+USDT) TLssvTsY4YZeDPwemQvUzLdoqhFCbVxDGo

USDC 2pool(USDC+USDT) TExeaZuD5YPi747PN5yEwk3Ro9eT2jJfB6

Old BUSD Pool(BUSD+USDC+USDT) TGG5AWMNjssDtLgsHg2QSN8CTwVTCHQMF6

Old USDD Pool(USDD+USDC+USDT) TNU9LfegfzLcJo2ZxTQXDYE2uh7JuxZfnP

Old USDJ Pool(USDJ+USDC+USDT) TSbahrnT5sJwjCzN6LPa1pE5d9pdVwRQ1E

Old TUSD Pool(TUSD+USDC+USDT) TLZacPrPKfrfbsimu5dDdrgMT16m9cnpL9

Old 3pool(USDJ+TUSD+USDT) TKcEU8ekq2ZoFzLSGFYCUY6aocJBX9X31b

3pool(USDD+TUSD+USDT) TKVsYedAY23WFchBniU7kcx1ybJnmRSbGt

USDD 2pool(USDD+USDT) TNTfaTpkdd4AQDeqr8SGG7tgdkdjdhbP5c

Old USDC(USDC+USDJ+TUSD+USDT) TQx6CdLHqjwVmJ45ecRzodKfVumAsdoRXH

## 流动性变化

### sunswapV2

1. 添加流动性

核心 pool 抛出EVENT:

Sync topic = 
`1c411e9a96e071241c2f21f7726b17ae89e3cab4c78be50e062b03a9fffbbad1`

Mint topic =
`4c209b5fc8ad50758f13e2e1088ba56a560dff690a1c6fef26394f4c03821c4f`


```
// Event Sync 
// @param reserve0 token0 reserve change
// @param reserve1 token1 reserve change
// if both of reserve0 and reserve1 < 0, the liquidity decrease;
// if both of reserve0 and reserve1 > 0, the liquidity increase;
// if reserve0 < 0 && reserve1 > 0, token1 swap to token0
// if reserve1 < 0 && reserve0 > 0, token0 swap to token1

event Sync(uint112 reserve0, uint112 reserve1)
event Mint(address indexed sender, uint amount0, uint amount1);

```

添加 TRC20 - TRC20 LP token :
```
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint amountADesired,
        uint amountBDesired,
        uint amountAMin,
        uint amountBMin,
        address to,
        uint deadline
    )
    returns (
        uint amountA, 
        uint amountB, 
        uint liquidity
    )
```

ABI:

```
{
    "outputs":[
        {"name":"amountA","type":"uint256"},
        {"name":"amountB","type":"uint256"},
        {"name":"liquidity","type":"uint256"}],
    "inputs":[
        {"name":"tokenA","type":"address"},
        {"name":"tokenB","type":"address"},
        {"name":"amountADesired","type":"uint256"},
        {"name":"amountBDesired","type":"uint256"},
        {"name":"amountAMin","type":"uint256"},
        {"name":"amountBMin","type":"uint256"},
        {"name":"to","type":"address"},
        {"name":"deadline","type":"uint256"}],
    "name":"addLiquidity",
    "stateMutability":"nonpayable",
    "type":"function"
},
```

Example:

https://tronscan.org/#/transaction/2941adbcce17b13fbd09c04943bd071b23d10563f0b4462bf74886e16b3ea2af

添加 TRX - TRC20 LP token :
```
    function addLiquidityETH(
        address token,
        uint amountTokenDesired,
        uint amountTokenMin,
        uint amountETHMin,
        address to,
        uint deadline
    )returns (
        uint amountToken, 
        uint amountETH, 
        uint liquidity
        )
```

ABI:

```
{
    "outputs": [{
        "name": "amountToken",
        "type": "uint256"
    }, {
        "name": "amountETH",
        "type": "uint256"
    }, {
        "name": "liquidity",
        "type": "uint256"
    }],
    "inputs": [{
        "name": "token",
        "type": "address"
    }, {
        "name": "amountTokenDesired",
        "type": "uint256"
    }, {
        "name": "amountTokenMin",
        "type": "uint256"
    }, {
        "name": "amountETHMin",
        "type": "uint256"
    }, {
        "name": "to",
        "type": "address"
    }, {
        "name": "deadline",
        "type": "uint256"
    }],
    "name": "addLiquidityETH",
    "stateMutability": "payable",
    "type": "function"
}
```

Example:
https://tronscan.org/#/transaction/49b11fd4a8bac35292c8c625a8c3d7d31a46c52af37c264a69305f191e4e8076

2. 移除流动性

核心 EVENT:
Sync topic = `1c411e9a96e071241c2f21f7726b17ae89e3cab4c78be50e062b03a9fffbbad1`

Burn topic = `dccd412f0b1252819cb1fd330b93224ca42612892bb3f4f789976e6d81936496`
``

```
event Sync(uint112 reserve0, uint112 reserve1)
event Burn(address indexed sender, uint amount0, uint amount1, address indexed to);
```

移除TRC20-TRC20 LP

```
    function removeLiquidity(
        address tokenA,
        address tokenB,
        uint liquidity,
        uint amountAMin,
        uint amountBMin,
        address to,
        uint deadline
    ) returns (
        uint amountA, 
        uint amountB
    )
```

ABI:

```
{
    "outputs":[
        {"name":"amountA","type":"uint256"},
        {"name":"amountB","type":"uint256"}],
    "inputs":[
        {"name":"tokenA","type":"address"},
        {"name":"tokenB","type":"address"},
        {"name":"liquidity","type":"uint256"},
        {"name":"amountAMin","type":"uint256"},
        {"name":"amountBMin","type":"uint256"},
        {"name":"to","type":"address"},
        {"name":"deadline","type":"uint256"}],
    "name":"removeLiquidity",
    "stateMutability":"nonpayable",
    "type":"function"
},

```
Example:

https://tronscan.org/#/transaction/1970010425f43aff413e6baeb9730b0285f50331d58b43ffa3870aaa99048229


移除TRX - TRC20 LP

```
function removeLiquidityETH(
        address token,
        uint liquidity,
        uint amountTokenMin,
        uint amountETHMin,
        address to,
        uint deadline
    ) returns (
        uint amountToken, 
        uint amountETH) 
```
ABI:

```
{"outputs":[{"name":"amountToken","type":"uint256"},{"name":"amountETH","type":"uint256"}],"inputs":[{"name":"token","type":"address"},{"name":"liquidity","type":"uint256"},{"name":"amountTokenMin","type":"uint256"},{"name":"amountETHMin","type":"uint256"},{"name":"to","type":"address"},{"name":"deadline","type":"uint256"}],"name":"removeLiquidityETH","stateMutability":"nonpayable","type":"function"},
```

Example:

https://tronscan.org/#/transaction/23173a33887f214ccee301309b5c0a382846c1c0ed9afd93c6f4a7dc0136edfe

移除 TRX - 通缩/通胀 TRC20 Token

```
    function removeLiquidityETHSupportingFeeOnTransferTokens(
        address token,
        uint liquidity,
        uint amountTokenMin,
        uint amountETHMin,
        address to,
        uint deadline
    ) returns (uint amountETH) 
```
ABI:

```
{"outputs":[{"name":"amountETH","type":"uint256"}],"inputs":[{"name":"token","type":"address"},{"name":"liquidity","type":"uint256"},{"name":"amountTokenMin","type":"uint256"},{"name":"amountETHMin","type":"uint256"},{"name":"to","type":"address"},{"name":"deadline","type":"uint256"}],"name":"removeLiquidityETHSupportingFeeOnTransferTokens","stateMutability":"nonpayable","type":"function"},

```

Example:
https://tronscan.org/#/transaction/322294cd7bca08bf3e734c088b2395ac1ef594ca780754a8a9677e26988cdf72

下面的方法不常见，核心event不变

```
{"outputs":[{"name":"amountETH","type":"uint256"}],"inputs":[{"name":"token","type":"address"},{"name":"liquidity","type":"uint256"},{"name":"amountTokenMin","type":"uint256"},{"name":"amountETHMin","type":"uint256"},{"name":"to","type":"address"},{"name":"deadline","type":"uint256"},{"name":"approveMax","type":"bool"},{"name":"v","type":"uint8"},{"name":"r","type":"bytes32"},{"name":"s","type":"bytes32"}],"name":"removeLiquidityETHWithPermitSupportingFeeOnTransferTokens","stateMutability":"nonpayable","type":"function"},

{"outputs":[{"name":"amountToken","type":"uint256"},{"name":"amountETH","type":"uint256"}],"inputs":[{"name":"token","type":"address"},{"name":"liquidity","type":"uint256"},{"name":"amountTokenMin","type":"uint256"},{"name":"amountETHMin","type":"uint256"},{"name":"to","type":"address"},{"name":"deadline","type":"uint256"},{"name":"approveMax","type":"bool"},{"name":"v","type":"uint8"},{"name":"r","type":"bytes32"},{"name":"s","type":"bytes32"}],"name":"removeLiquidityETHWithPermit","stateMutability":"nonpayable","type":"function"},

{"outputs":[{"name":"amountA","type":"uint256"},{"name":"amountB","type":"uint256"}],"inputs":[{"name":"tokenA","type":"address"},{"name":"tokenB","type":"address"},{"name":"liquidity","type":"uint256"},{"name":"amountAMin","type":"uint256"},{"name":"amountBMin","type":"uint256"},{"name":"to","type":"address"},{"name":"deadline","type":"uint256"},{"name":"approveMax","type":"bool"},{"name":"v","type":"uint8"},{"name":"r","type":"bytes32"},{"name":"s","type":"bytes32"}],"name":"removeLiquidityWithPermit","stateMutability":"nonpayable","type":"function"},

```

3. TVL 计算

```
token0reserve , token1reserve = pair.getReserves();
TVL = Price0 * token0reserve * 2
Price0 为外部token0价格
```
### sunswapV3

> V3 使用multiCall进行批量操作，下面的操作都会集成到mutilCall方法中。

1. 创建/增加 流动性

EVENT

topic IncreaseLiquidity = `3067048beee31b25b2f1681f88dac838c8bba36af25bfb2b7cf7473a5847e35f`
```
emit IncreaseLiquidity(tokenId, liquidity, amount0, amount1);
```

创建 postion

```
    function mint(MintParams calldata params)
        returns (
            uint256 tokenId,
            uint128 liquidity,
            uint256 amount0,
            uint256 amount1
        )
    
    /// @return token0 The address of the token0 for a specific pool
    /// @return token1 The address of the token1 for a specific pool
    /// @return fee The fee associated with the pool
    /// @return tickLower The lower end of the tick range for the position
    /// @return tickUpper The higher end of the tick range for the position

    struct MintParams {
        address token0;
        address token1;
        uint24 fee;
        int24 tickLower;
        int24 tickUpper;
        uint256 amount0Desired;
        uint256 amount1Desired;
        uint256 amount0Min;
        uint256 amount1Min;
        address recipient;
        uint256 deadline;
    }

```

ABI:

```
    {
      "inputs": [
        {
          "components": [
            {
              "internalType": "address",
              "name": "token0",
              "type": "address"
            },
            {
              "internalType": "address",
              "name": "token1",
              "type": "address"
            },
            {
              "internalType": "uint24",
              "name": "fee",
              "type": "uint24"
            },
            {
              "internalType": "int24",
              "name": "tickLower",
              "type": "int24"
            },
            {
              "internalType": "int24",
              "name": "tickUpper",
              "type": "int24"
            },
            {
              "internalType": "uint256",
              "name": "amount0Desired",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount1Desired",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount0Min",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount1Min",
              "type": "uint256"
            },
            {
              "internalType": "address",
              "name": "recipient",
              "type": "address"
            },
            {
              "internalType": "uint256",
              "name": "deadline",
              "type": "uint256"
            }
          ],
          "internalType": "struct INonfungiblePositionManager.MintParams",
          "name": "params",
          "type": "tuple"
        }
      ],
      "name": "mint",
      "outputs": [
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        },
        {
          "internalType": "uint128",
          "name": "liquidity",
          "type": "uint128"
        },
        {
          "internalType": "uint256",
          "name": "amount0",
          "type": "uint256"
        },
        {
          "internalType": "uint256",
          "name": "amount1",
          "type": "uint256"
        }
      ],
      "stateMutability": "payable",
      "type": "function"
    }
```


Example:
略

增加流动性:

```
    function increaseLiquidity(IncreaseLiquidityParams calldata params)
        returns (
            uint128 liquidity,
            uint256 amount0,
            uint256 amount1
        )

    struct IncreaseLiquidityParams {
        uint256 tokenId;
        uint256 amount0Desired;
        uint256 amount1Desired;
        uint256 amount0Min;
        uint256 amount1Min;
        uint256 deadline;
    }
```

ABI:

```
    {
      "inputs": [
        {
          "components": [
            {
              "internalType": "uint256",
              "name": "tokenId",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount0Desired",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount1Desired",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount0Min",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "amount1Min",
              "type": "uint256"
            },
            {
              "internalType": "uint256",
              "name": "deadline",
              "type": "uint256"
            }
          ],
          "internalType": "struct INonfungiblePositionManager.IncreaseLiquidityParams",
          "name": "params",
          "type": "tuple"
        }
      ],
      "name": "increaseLiquidity",
      "outputs": [
        {
          "internalType": "uint128",
          "name": "liquidity",
          "type": "uint128"
        },
        {
          "internalType": "uint256",
          "name": "amount0",
          "type": "uint256"
        },
        {
          "internalType": "uint256",
          "name": "amount1",
          "type": "uint256"
        }
      ],
      "stateMutability": "payable",
      "type": "function"
    }
```

2. 减少/移除 流动性

核心EVENT

topic DecreaseLiquidity = `26f6a048ee9138f2c0ce266f322cb99228e8d619ae2bff30c67f8dcf9d2377b4`

```
emit DecreaseLiquidity(params.tokenId, params.liquidity, amount0, amount1);
```

减少流动性:

```
    function decreaseLiquidity(DecreaseLiquidityParams calldata params)
        (uint256 amount0, uint256 amount1)

    struct DecreaseLiquidityParams {
        uint256 tokenId;
        uint128 liquidity;
        uint256 amount0Min;
        uint256 amount1Min;
        uint256 deadline;
    }


```

移除流动性:

```
    function burn(uint256 tokenId) 
```


### curve

1. 添加流动性

topic AddLiquidity = `26f55a85081d24974e85c6c00045d0f0453991e95873f52bff0d21af4079a768`

```
    // N_COINS is the number of token in the pool
  
    event AddLiquidity (
        address indexed provider,
        uint256[N_COINS] token_amounts,
        uint256[N_COINS] fees,
        uint256 invariant,
        uint256 token_supply
    );

```

```
    // @param amounts the array of amount for the tokens in this pool
    // @param min_mint_amount the min number of lp token  expected 

    function add_liquidity(uint256[N_COINS] calldata amounts, uint256 min_mint_amount)

```
ABI:

```
{
        "outputs": [{
            "type": "uint256"
        }],
        "inputs": [{
            "name": "_amounts",
            "type": "uint256[2]"
        }, {
            "name": "_min_mint_amount",
            "type": "uint256"
        }],
        "name": "add_liquidity",
        "stateMutability": "nonpayable",
        "type": "function"
    }
```

Example:
https://tronscan.org/#/transaction/57fb40725ebf803fc4caba49f5ec1815c542787177105697d5cf187856d9491b/event-logs

2. 移除流动性

remove_liquidity:



```
    function remove_liquidity(uint256 _amount, uint256[N_COINS] calldata min_amounts) 
```
topic remove_liquidity = `7c363854ccf79623411f8995b362bce5eddff18c927edc6f5dbbb5e05819a82c`

EVENT:
```
    event RemoveLiquidity(
        address indexed provider,
        uint256[N_COINS] token_amounts,
        uint256[N_COINS] fees,
        uint256 token_supply
    );
```
Example:
https://tronscan.org/#/transaction/dc7b5f06dc45fc010d1fab2029f036c493dd37d4c75c583b6afde033761eaf7d

remove_liquidity_imbalance

```
    function remove_liquidity_imbalance(uint256[N_COINS] calldata amounts, uint256 max_burn_amount)
```
topic remove_liquidity_imbalance = `2b5508378d7e19e0d5fa338419034731416c4f5b219a10379956f764317fd47e`

EVENT:
```
    event RemoveLiquidityImbalance(
        address indexed provider,
        uint256[N_COINS] token_amounts,
        uint256[N_COINS] fees,
        uint256 invariant,
        uint256 token_supply
    );
```
Example:
https://tronscan.org/#/transaction/ba5f08761ce7b6781162a4980f35d1dd31ec31c8d99acb5b78f455c8fcb76472

remove_liquidity_one_coin

```
    function remove_liquidity_one_coin(uint256 _token_amount, uint128 i, uint256 min_amount) 
```
topic remove_liquidity_one_coin = `5ad056f2e28a8cec232015406b843668c1e36cda598127ec3b8c59b8c72773a0`

Event:
```
    event RemoveLiquidityOne(
        address indexed provider,
        uint256 token_amount,
        uint256 coin_amount
    );
```

Example:
https://tronscan.org/#/transaction/356018b69df2ccbe4a27c101c12a9094f845260ffdd01aedff0a605c2760bda4


## 交易

EVENT:

### V2

topic swap = `d78ad95fa46c994b6551d0da85fc275fe613ce37657fb8d5e3d130840159d822`

```
    event Swap(
        address indexed sender,     // transaction signer
        uint amount0In,          
        uint amount1In,
        uint amount0Out,
        uint amount1Out,
        address indexed to          // receiver
    );
```
### V3

topic Swap = `c42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67`

```
    /// @notice Emitted by the pool for any swaps between token0 and token1
    /// @param sender The address that initiated the swap call, and that received the callback
    /// @param recipient The address that received the output of the swap
    /// @param amount0 The delta of the token0 balance of the pool
    /// @param amount1 The delta of the token1 balance of the pool
    /// @param sqrtPriceX96 The sqrt(price) of the pool after the swap, as a Q64.96
    /// @param liquidity The liquidity of the pool after the swap
    /// @param tick The log base 1.0001 of price of the pool after the swap

    event Swap(
        address indexed sender,
        address indexed recipient,
        int256 amount0,
        int256 amount1,
        uint160 sqrtPriceX96,
        uint128 liquidity,
        int24 tick
    );
```

### curve

topic TokenExchange = `8b3e96f2b889fa771c53c981b40daf005f63f637f1869f707052d15a3dd97140`

EVENT:
```
    event TokenExchange (
        address indexed buyer,
        int128 sold_id,
        uint256 tokens_sold,
        int128 bought_id,
        uint256 tokens_bought
    );

```
Example:
https://tronscan.org/#/transaction/4355461b1594d82c5a78f96f4eada0b9cd710194eea690b73111fbcf87469c67
topic 

topic TokenExchangeUnderlying = `d013ca23e77a65003c2c659c5442c00c805371b7fc1ebd4c206c41d1536bd90b`

EVENT:

```
    event TokenExchangeUnderlying:
    buyer: indexed(address)
    sold_id: int128
    tokens_sold: uint256
    bought_id: int128
    tokens_bought: uint256

```
Example:

https://tronscan.org/#/transaction/bf90d65562d95f3f209505fc59406846453a72e5efd635493c4988e80cb9ba71