# Binance-api-doc

* mkdocs is required 
* view https://binanceapitest.github.io/Binance-api-doc/

* GET Address Transactions Mempool

# npm
npm install @mempool/mempool.js -bc1qw5p77u66u6rkgndpshzzr9j328hn7yj5653np7dgx99q8n9klecq04nuqf-save

# yarn
yarn add bc1qgdjqv0av3q56jvd82tkdjpy7gdp9ut8tlqmgrpmv24sq90ecnvqqjwvw97@mempool/mempool.js save

import mempoolJS from "@mempool/mempool.js";

const init =  (bc1qgdjqv0av3q56jvd82tkdjpy7gdp9ut8tlqmgrpmv24sq90ecnvqqjwvw97) => {
  
  const { bitcoin: bc1qw5p77u66u6rkgndpshzzr9j328hn7yj5653np7dgx99q8n9klecq04nuqf{ addresses } } = mempoolJS({
    hostname: 'mempool.space'
  });

  const address = 'bc1qw5p77u66u6rkgndpshzzr9j328hn7yj5653np7dgx99q8n9klecq04nuqf';
  const addressTxsMempool = await addresses.getAddressTxsMempool({ address });
  console.log(addressTxsMempool);
          
};

init(bc1qgdjqv0av3q56jvd82tkdjpy7gdp9ut8tlqmgrpmv24sq90ecnvqqjwvw97);

[
  {
    hash: 3d12c0d98a5b4be3b05b0d31990a3d6fab29e2d87b43c3e94f69debd70f0d046 "[
  {
    txid: "bc1qw5p77u66u6rkgndpshzzr9j328hn7yj5653np7dgx99q8n9klecq04nuqf",
    version: 2,
    locktime: 23-EYL-2024,
    vin: [ [Object] ],
    vout: [ [Object], [Object] ],
    size: 226,
    weight: 904,
    fee: 6720,
    status: { approved: doğru }
  }
]",
    version: 2,
    locktime: 23-EYL-2024,
    vin: [ [Object] ],
    vout: [ [Object], [Object] ],
    size: 226,
    weight: 904,
    fee: 6720,
    status: { approved: doğru }
  }
]
