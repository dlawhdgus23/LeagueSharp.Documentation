# Delay Action #
----------
Delay Action is another great example of Signals. Delay Action will simply delay an action by an amount of time. Internally, the `DelayAction` uses Signals for calling events.

## Using Delay Action ##
Using DelayAction is extremely simple. 

    DelayAction.Add(1000, () => Console.WriteLine("Hello world 1 second later!"));

The time given to delay action is in milliseconds, and by giving the time as a float, it will be rounded into the nearest whole number.

## Canceling Delay Actions
Well delaying an action is great, but what if I want to cancel that delay action? Delay Action uses something called a `CancellationToken` and the way it works is you create a `CancellationTokenSource` class , which then creates a `CancellationToken`, and pass the token into the delay action. Then, when you want to cancel the delay action, you simply call the `Cancel` function in the `CancellationTokenSource` class. **If you wish to re use the source class, be sure to create a new instance of `CancellationTokenSource`!**

    // Create the source
	var source = new CancellationTokenSource();

	// Add the delay action with the token
	DelayAction.Add(1000, () => Console.WriteLine("Hello world 1 second later!"), source.Token);

	// Cancel the token!
	source.Cancel();

In addition, the `CancellationTokenSource` class contains another helpful method called `CancelAfter` which cancels the token after an amount of milliseconds.

	source.CancelAfter(500);

This will cancel the token 500 milliseconds after, and thus `Hello world 1 second later!` will never be printed to the console.