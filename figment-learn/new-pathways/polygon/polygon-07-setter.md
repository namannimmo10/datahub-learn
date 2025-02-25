At this point we have deployed a smart contract on the Polygon testnet and we have a client side application that's ready to interact with it. We just need to wire up the last part! We built a simple page on the last step to help you interact with the smart contract. Since the contract has only two methods (`set` and `get`) that's all the UI will do: set a number through the smart contract.

As simple as it sounds, what's happening in the background is actually very powerful: we're using the Polygon blockchain to store information (in this example, a number) and we're using a smart contract as an interface to read and write that information to the blockchain. What's crucial is that all this is happening without having to spin up a database and an API... So let's go!

-------------------------------------

# The Challenge

{% hint style="tip" %}
In the file `components/protocols/polygon/SeStorage.tsx`, implement the `setValue` function.    
{% endhint %}

**Take a few minutes to figure this out.**

```typescript
	const setValue = async () => {
		setFetchingSet(true);
		setTxHash(null);
	
		const provider = new ethers.providers.Web3Provider(window.ethereum);
		const signer = provider.getSigner();
		// Try to figure out the expected parameters
		const contract = new ethers.Contract(undefined);
		
		try {
			// Try to figure out the expected method 
			const transactionResult = undefined;

			setFetchingSet(false);
			setInputNumber(0);
			setConfirming(true);
			const receipt = await transactionResult.wait();
			setTxHash(receipt.transactionHash);
			setConfirming(false);
		} catch(error) {
			console.log(error);
			setFetchingSet(false);
		}
	}
```


Need some help? Check out these two tips/links  
* [**Create a Contract using ethers**](https://docs.ethers.io/v5/api/contract/contract/#Contract--creating) 
	* You can **console.log `SimpleStorageJson`** to find the contract's `abi` and `address` (through the property `networks`)  
* [**How to call a contract's methods on a ethers Contract object**](https://docs.ethers.io/v5/api/contract/contract/#Contract-functionsCall)  
* To read from the blockchain you don't need to spend any tokens so you can just use a provider to create a Contract instance. But to write you will need to create and sign a transaction through Metamask. Use a `signer` to create the Contract object!

{% hint style="info" %}
You can [**join us on Discord**](https://discord.gg/fszyM7K), if you have questions or want help completing the tutorial.
{% endhint %}

Still not sure how to do this? No problem! The solution is below so you don't get stuck.

-------------------------------------

# The solution

```typescript
	const setValue = async () => {
		setFetchingSet(true);
		setTxHash(null);
	
		const provider = new ethers.providers.Web3Provider(window.ethereum);
		const signer = provider.getSigner();
		const contract = new ethers.Contract(
			SimpleStorageJson.networks['80001'].address,
			SimpleStorageJson.abi,
			signer
		);
		try {
			const transactionResult = await contract.set(inputNumber);
			setFetchingSet(false);
			setInputNumber(0);
			setConfirming(true);
			const receipt = await transactionResult.wait();
			setTxHash(receipt.transactionHash);
			setConfirming(false);
		} catch(error) {
			console.log(error);
			setFetchingSet(false);
		}
	}
```

**What happened in the code above?**

* We create Contract objects using
  * The contract JSON's address.
  * The contract JSON's ABI.
  * A signer, from the ethers web3 provider.
* We then call the function `set` on this Contract object to operate on our decentralized code. The names of the functions must match the ones we defined in our Solidity smart contract. These are available via the ABI.

-----------------------------

# Make sure it works

Once the code above has been saved, you can click and this is what the UI should look like!

![](../../../.gitbook/assets/polygon-setter-v21.gif)

-------------------------------------

# Conclusion

Now that we've set the storage of our contract, we can read it. We're going to learn how to do this in the final tutorial of the pathway.
