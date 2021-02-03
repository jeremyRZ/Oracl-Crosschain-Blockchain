# Oracl-Crosschain-Blockchain

**Introductin**
Blockchain has rapidly aroused the interests across the global construction industry, as it can enable a collaborative and trusting environment throughout the project lifecycle. However, such promises cannot be achieved spontaneously without blockchain “oracles” used to bridge the on-chain and off-chain worlds.

## Crosschain Demo

#### Project realization process
1. Clean Up
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/1.png)
1. Start the network and create the first channel (my channel).
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/2.png)
1. Create the second channel (newchannel).
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/3.png)
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/4.png)
1. Deploy fabcar to mychannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/5.png)
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/6.png)
1. Deploy basic to newchannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/7.png)
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/8.png)
1. Invoke a transaction that initializes the fabcar chaincode on mychannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/9.png)
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/10.png)
1. Invoke a transaction that initializes the basic chaincode on newchannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/11.png)
1. Query all cars in fabcar on mychannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/12.png)
1. Query asset6 in basic on newchannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/13.png)
1. Retrieve asset6 from basic on newchannel and store it to fabcar on mychannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/14.png)
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/15.png)
1. Query all cars in fabcar on mychannel Asset6 in basic on newchannel is now stored on fabcar on mychannel.
![P1](https://raw.githubusercontent.com/jeremyRZ/Oracl-Crosschain-Blockchain/main/Screen%20Shot/16.png)

#### CrossChain Code
```javascript
async getBasicValue(ctx, carNumber){
      const cc1Args = ['ReadAsset', 'asset6'];
      const cc1Res = await ctx.stub.invokeChaincode('basic', cc1Args, 'newchannel');
      console.log(cc1Res)
      if (cc1Res.status !== 200) {
        throw new Error(cc1Res.message);
      }
      const cc1Asset = JSON.parse(cc1Res.payload.toString('utf8'));
      await ctx.stub.putState(carNumber, Buffer.from(JSON.stringify(cc1Asset)));
    }

```