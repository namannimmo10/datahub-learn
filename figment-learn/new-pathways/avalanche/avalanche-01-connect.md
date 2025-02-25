[Avalanche.js](https://github.com/ava-labs/avalanchejs) is a client JavaScript package that makes it easy to interact with Avalanche blockchain nodes, query data, submit transactions and offers plenty of other functionality. It's the official package developed by Avalanche, and is a preferred method of communicating with nodes on the private or public networks for development purposes.

In this tutorial, we will learn how to connect to an Avalanche node using DataHub. You will need to complete the code in each tutorial, to make the dApp functional.  

------------------------

# Challenge

{% hint style="tip" %}
In `pages/api/avalanche/connect.ts`, implement the function and try to establish your first connection to the Avalanche network. To verify your connection has been correctly established, try to return the current protocol version. You must replace any instances of `undefined` with working code to accomplish this.
{% endhint %}

```typescript
//...
  try {
    const client = undefined;
    const info = undefined;
    const version = undefined;
    res.status(200).json(version);
  }
//...
```

**Need some help?** Check out these tips
* [**Check out the `AvalancheJS` library**](https://github.com/ava-labs/avalanchejs)
* Use the `getAvalancheClient` helper function.
* Use the `Info` method on the client.
* Use the `getNodeVersion` method on the client info (remember to `await` this call).

{% hint style="info" %}
You can [**join us on Discord**](https://discord.gg/fszyM7K), if you have questions or want help completing the tutorial.
{% endhint %}

Still not sure how to do this? No problem! The solution is below so you don't get stuck.

------------------------

# Solution

```typescript
//...
  try {
    const client = getAvalancheClient();
    const info = client.Info();
    const version = await info.getNodeVersion();
    res.status(200).json(version);
  }
//...
```

**What happened in the code above?**

* We instantiate an `Avalanche` object with `getAvalancheClient`.
* Calling the `Info` method on the `AvalancheClient` module returns a reference to the Info RPC.
* `getNodeVersion` sends the request and retrieves the current version of Avalanche running on the node.

------------------------

# Make sure it works

Once the code is complete and the file has been saved, refresh the page to see it update & display the current version.

![](../../../.gitbook/assets/pathways/avalanche/avalanche-connect.gif)

-------------------------

# Conclusion

Now that we have successfully connected to Avalanche node using DataHub, we are ready to move onto the next tutorial. We have also created the foundation for the next step, creating an account.

