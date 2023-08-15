Update:- We received 1st position for Sponsor Challenge Category => https://devpost.com/software/xpanse

Xpanse
==================

The Yield Optimizer on NEAR Protocol.

xpanse provides strategies that offers best returns on your assets across near protocol.

![Xpanse](https://user-images.githubusercontent.com/85037852/154845518-6d8f20de-be99-412c-b5f1-6e59400d56e7.jpg)

Inspiration
==================
We are currently two members.
1. Kartik: Started the journey into web3 through the NEAR Metabuild Hackathon. It contained several beginner friendly challenges.  
2. Coco: He has experience in building dapps on solidity, He has written yield optimization strategies on ethereum.

After hours of discussion and research, the team decided to work on Auto-compounding challenge from REF Finance. The challenge was interesting to work on with a lot of future potential. Also being an avid stock trader this seemed most relatable ( because of AMM ).

What it does
==================
It optmizes the yield for a ref finance farm using auto-compounding strategy.

How we built it
==================
We used rust and react to build it.

Challenges we ran into
==================
- Working on and implementing Cross-Contract Calls was difficult. Asking questions on Discord server came in handy when we were stuck on a callback issue.
- We saw a lot of 'Exceeded the Prepaid Gas' Error. To tackle this we had to divide the code into several steps. For example, The complete harvesting process consists of 5 steps i.e. 5 Cron calls.

What we learned
==================
Learn and Build was our slogan throughout the journey. Not being familiar with NEAR concepts a lot of research was needed. Plan was to spend some time on the NEAR Docs, go through the Excellent tutorials there and then the SDK Docs. For the building Phase, We decided to first work on Harvesting code. The complete harvesting process was divided into several steps:

- Claiming Rewards from the farm.
- Withdrawing them to Near wallet.
- Deposit Back to Ref.
- Swapping Rewards for Pool Tokens.
- Adding Liquidity
- Staking the new seeds into Farms
  
Next we worked on User Deposit and Withdraws Funds Code. Correctly deciding the states for contract was the crucial step here. Next came making a UI for the Contract. Not being familiar with the UI frameworks, this was challenging but with the help of stackoverflow and the official docs this task was also conqured.

Accomplishments that we're proud of
==================
- We wrote our first auto-compounding strategy for yield optmization
- Made a basic UI for this

What's next for Xpanse
==================
- We will be adding more strategies, the next will be using harvested rewards in some other pool which high APR than the current one.
- And then we will try to improve and optimize.

Commands for using this strategy from near-cli
===========

- Deposit token to strategy
```
near call exchange.ref-dev.testnet mft_transfer_call '{"token_id": ":107", "receiver_id": "xpanse-strategy.testnet","amount":"1000000000000000000", "msg":""}' --account_id <sender-id>.testnet --depositYocto '1'  --gas '300000000000000'
```

- Withdraw token from strategy
```
near call xpanse-strategy.testnet '{"amount": "1000000000000000000"}' --account_id <sender-id> --depositYocto '1'  --gas '300000000000000'
```

- Harvesting calls
```
near call contract.name.testnet harvesting_step_1 --account-id <sender-id>.testnet --gas '300000000000000'
near call contract.name.testnet harvesting_step_2 --account-id <sender-id>.testnet --gas '300000000000000'
near call contract.name.testnet harvesting_step_3 --account-id <sender-id>.testnet --gas '300000000000000'
near call contract.name.testnet harvesting_step_4 --account-id <sender-id>.testnet --gas '300000000000000'
near call contract.name.testnet harvesting_step_5 --account-id <sender-id>.testnet --gas '300000000000000'
near call contract.name.testnet harvesting_step_6 --account-id <sender-id>.testnet --gas '300000000000000'
```

Quick Start
===========

To run this project locally:

1. Prerequisites: Make sure you've installed [Node.js] ≥ 12
2. Install dependencies: `yarn install`
3. Run the local development server: `yarn dev` (see `package.json` for a
   full list of `scripts` you can run with `yarn`)

Now you'll have a local development environment backed by the NEAR TestNet!

Go ahead and play with the app and the code. As you make code changes, the app will automatically reload.


Exploring The Code
==================

1. The "backend" code lives in the `/contract` folder. See the README there for
   more info.
2. The frontend code lives in the `/src` folder. `/src/index.html` is a great
   place to start exploring. Note that it loads in `/src/index.js`, where you
   can learn how the frontend connects to the NEAR blockchain.
3. Tests: there are different kinds of tests for the frontend and the smart
   contract. See `contract/README` for info about how it's tested. The frontend
   code gets tested with [jest]. You can run both of these at once with `yarn
   run test`.


Deploy
======

Every smart contract in NEAR has its [own associated account][NEAR accounts]. When you run `yarn dev`, your smart contract gets deployed to the live NEAR TestNet with a throwaway account. When you're ready to make it permanent, here's how.


Step 0: Install near-cli (optional)
-------------------------------------

[near-cli] is a command line interface (CLI) for interacting with the NEAR blockchain. It was installed to the local `node_modules` folder when you ran `yarn install`, but for best ergonomics you may want to install it globally:

    yarn install --global near-cli

Or, if you'd rather use the locally-installed version, you can prefix all `near` commands with `npx`

Ensure that it's installed with `near --version` (or `npx near --version`)


Step 1: Create an account for the contract
------------------------------------------

Each account on NEAR can have at most one contract deployed to it. If you've already created an account such as `your-name.testnet`, you can deploy your contract to `xpanse.your-name.testnet`. Assuming you've already created an account on [NEAR Wallet], here's how to create `xpanse.your-name.testnet`:

1. Authorize NEAR CLI, following the commands it gives you:

      near login

2. Create a subaccount (replace `YOUR-NAME` below with your actual account name):

      near create-account xpanse.YOUR-NAME.testnet --masterAccount YOUR-NAME.testnet


Step 2: set contract name in code
---------------------------------

Modify the line in `src/config.js` that sets the account name of the contract. Set it to the account id you used above.

    const CONTRACT_NAME = process.env.CONTRACT_NAME || 'xpanse.YOUR-NAME.testnet'


Step 3: deploy!
---------------

One command:

    yarn deploy

As you can see in `package.json`, this does two things:

1. builds & deploys smart contract to NEAR TestNet
2. builds & deploys frontend code to GitHub using [gh-pages]. This will only work if the project already has a repository set up on GitHub. Feel free to modify the `deploy` script in `package.json` to deploy elsewhere.


Troubleshooting
===============

On Windows, if you're seeing an error containing `EPERM` it may be related to spaces in your path. Please see [this issue](https://github.com/zkat/npx/issues/209) for more details.


  [React]: https://reactjs.org/
  [create-near-app]: https://github.com/near/create-near-app
  [Node.js]: https://nodejs.org/en/download/package-manager/
  [jest]: https://jestjs.io/
  [NEAR accounts]: https://docs.near.org/docs/concepts/account
  [NEAR Wallet]: https://wallet.testnet.near.org/
  [near-cli]: https://github.com/near/near-cli
  [gh-pages]: https://github.com/tschaub/gh-pages
