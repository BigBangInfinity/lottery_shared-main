Clone three repos to these folders:

```
C:\> git clone https://github.com/BigBangInfinity/lottery_shared-contracts
C:\> git clone https://github.com/BigBangInfinity/lottery_shared-scaffold-eth-2
```

npm/yarn install in these folders

use npm for lottery_shared-contracts and yarn for lottery_shared-scaffold-eth-2 because this is what I used for these folders.

```
C:\lottery_shared-contracts> npm install
C:\lottery_shared-scaffold-eth-2> yarn install
```

Compile contract

```
C:\lottery_shared-contracts> npx hardhat compile
```

Deploy lottery contract:

```
C:\lottery_shared-contracts>npx ts-node .\scripts\deployLottery.ts
```

Lottery contract deployed at 0xED120a0e0B5E95BbC51549f58aa7131C53Dc67fB

Token contract deployed at 0xB0eF8f57B5cE9eA614a7f24d74D471E8Cf90974e

verify on etherscan:
```
C:\lottery_shared-contracts>npx hardhat verify --network sepolia 0xED120a0e0B5E95BbC51549f58aa7131C53Dc67fB "LotteryToken" "LT0" "1000" "1000000000000000000" "200000000000000011" 
C:\lottery_shared-contracts>npx hardhat verify --network sepolia 0xB0eF8f57B5cE9eA614a7f24d74D471E8Cf90974e "LotteryToken" "LT0"
```

The ABI of files
```
C:\lottery_shared-contracts\artifacts\contracts\Lottery.sol\Lottery.json
C:\lottery_shared-contracts\artifacts\contracts\LotteryToken.sol\LotteryToken.json
```

should be copied into 

```
C:\lottery_shared-scaffold-eth-2\packages\nextjs\abis
```

update environment variables in C:\lottery_shared-scaffold-eth-2\packages\nextjs\.env.local

```
NEXT_PUBLIC_TOKEN_ADDRESS = "0xB0eF8f57B5cE9eA614a7f24d74D471E8Cf90974e"
NEXT_PUBLIC_LOTTERY_ADDRESS = "0xED120a0e0B5E95BbC51549f58aa7131C53Dc67fB"
```

Launch frontend
```
C:\lottery_shared-scaffold-eth-2> yarn start
```

Only owner (deployer) can open bets


![image](https://github.com/BigBangInfinity/lottery_shared-main/assets/37957341/a21027a1-7ca5-4d02-9ce2-f9a1a749000c)

buy tokens (1000 tokens per ETH)

![image](https://github.com/BigBangInfinity/lottery_shared-main/assets/37957341/2f70718d-d9aa-48cb-ae74-9972249fa763)


Approve Lottery contract to spend token

![image](https://github.com/BigBangInfinity/lottery_shared-main/assets/37957341/291e55fc-8d06-4efe-b25e-4a8b2091b6e4)

make bets (1.2 tokens per bet) 

![image](https://github.com/BigBangInfinity/lottery_shared-main/assets/37957341/d5082ede-cb85-40e4-afe9-b5e7bc89086c)

after the lottery expired, anyone can close lottery. The winner can claim the price. Only owner can withdraw from owner pool.
