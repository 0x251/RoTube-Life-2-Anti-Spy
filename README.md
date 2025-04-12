### RoTube Life 2 Anti Remote Spy
Rotube main focus seems to be on preventing remote spying, and it has seemed to work well, as most people don't know how to "bypass" it.
But, it's very easy to understand, this concept "Remotes always are fired, as the client has to send something to the server, so no matter what they can do to obsecure it, they can't change the fact that the client has to send something to the server.". To keep this in mind this reversal will be on my understanding of there network module.


### Understanding RoTube Life 2 Network Module (Chapter 1)
Lets try and see how remotes are being fired in rspy, (hydroxide was having issues, so will not be using it for this, as we will only be using it once).
As we can see in the image below, a remote 


```lua
game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.4.4"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("whutthe so pro \240\159\152\169"):WaitForChild("whutthe so pro \240\159\152\169"):WaitForChild("whutthe so pro \240\159\152\169"):InvokeServer()
```


 is being fired, as invokeServer(), this seems to be the case for all remotes, so therefore you can't really see,
The remote name or the arg's it takes, so the best approcach is to use "SaveInstance", so we can really see what's going on.


![image](https://files.catbox.moe/t6yci7.png)


from this string "sleitnick_knit@1.4.4" we know that the remote is being triggered by knit, we can also confirm this by how the game loads by there loading screen.


![image](https://files.catbox.moe/ixk721.png)

![image](https://files.catbox.moe/ahzxn5.png)
![image](https://files.catbox.moe/rvjhek.png)


^ This is the loading screen, as you can see it's loading knit, so we know that knit is there network controller.

### Chapter 2 - The Network Controller (Knit) Handling Events / FireServer()
Lets get started on how Knit handles events as we can see here, they take fireServer(), with the arg's that are passed in, now lets see how we can actually fire a remote
We will jump to a script that handles input for the Maid's, and see how they handle it going to the network controller.


![image](https://files.catbox.moe/hqweo0.png)


![image](https://files.catbox.moe/m56nvs.png)

Now in the above image we can see, that we have a var called ``v_u_28`` which is defined as ``v_u_24.Bindable()`` now what is ``v_u_24``?
We can see here


```lua
local v_u_24 = shared.std
local v_u_25 = v_u_24.Knit
game:GetService("ContextActionService")
game:GetService("GuiService")
local v_u_26 = game:GetService("UserInputService")
local v_u_27 = require(script.Effects)
local v_u_28 = v_u_24.Bindable()
```

We can see it's ``shared.std`` now what is ``shared``?
we can find it here searching for ``std`` 
```lua
game:GetService("ReplicatedStorage").Shared.std
``` 

Now let's see what is available in ``shared.std``

![image](https://files.catbox.moe/8c1hnq.png)
As we see here, ``Bindable()`` is available, therefore in theory we can use ``require`` to call Bindable()
```lua
local Network = require(game:GetService("ReplicatedStorage").Shared.std)
``` 

Now we can access the ``Network`` module, and use ``FireServer()`` in theory,

```lua
local Network = require(game:GetService("ReplicatedStorage").Shared.std)
local Bind = Network.Bindable()
```

now we can also use controllers like ``print(Network.Knit.GetController("DataController"):Get("/System/Flags/PendingLikeChests"))`` and that will return a bool or


```lua
local Network = require(game:GetService("ReplicatedStorage").Shared.std)

-- local Bind = Network.Bindable()


table.foreach(Network.Knit.GetController("DataController"):Get("/System/Components/PCParts"), print)
```

this will return the current user's PC parts


For FireServer() you will need to use the controller and connect to it for the remote to fire, in this example https://github.com/Sleitnick/Knit/blob/main/test/client/KnitClientTest.client.luau


Anywas that's pretty much it, don't forget that nothing is ever hidden, you can always find a way to reverse things - 0x251


