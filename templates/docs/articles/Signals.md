# Signals #
----------
Signals are a great way to do actions when there is a certain condition (This condition is called the `SignalWaver`). An example for LeagueSharp projects might be to pop a health potion if the players health is below 30%. Signals are very customizable, they allow for developers to enable them, disable them, set an expiration, events for being raised, events for being disabled/enabled, and allowing you to reuse signals even after they have been called.

## Creating a Signal ##
Signals are created by calling `Signal.Create()`. **The `Signal.Create()` also returns the signal it created**, and allows you to subscribe to the events, enable/disable the event, etc.

    Signal.Create(delegate(object sender, Signal.RaisedArgs raisedArgs)
    {
    	var healthPotItem = ObjectManager.Player.InventoryItems.FirstOrDefault(item => item.Id == ItemId.Health_Potion);
    
    	// Check if the player has a health pot
    	if (healthPotItem != null)
    	{
    		// Use the health pot
    		ObjectManager.Player.Spellbook.CastSpell(healthPotItem.SpellSlot);
    	}
    
    	// Reset the signal, allowing it to be called again.
    	raisedArgs.Signal.Reset();
    },
    // Signal gets called when the players health percent is less then 45 %
    signal => ObjectManager.Player.HealthPercent < 30);

**Don't forget to call `Signal.Reset()` if you wish for your signal to not be destroyed when it is called! By default, a signal is removed once it is called.** The `Signal.RaisedArgs` class allows you to access the signal.

To create a signal with an expiration, pass in a DateTimeOffset as the next argument. By not adding an expiration, the signals will not expire.

	// Signal gets called when the players health percent is less then 30 %
    signal => ObjectManager.Player.HealthPercent < 30, DateTimeOffset.Now.AddMinutes(20));

In addition, signals also have "properties". These properties are dictionaries, and can be used to store information needed when the signal is raised that otherwise is not available. You can pass in a dictionary with values to be used by the signal.

			var propertiesDictionary = new Dictionary<string, object>();
            propertiesDictionary.Add("HealthPercent", 35);

            Signal.Create(delegate(object sender, Signal.RaisedArgs raisedArgs)
            {
                var healthPotItem =
                    ObjectManager.Player.InventoryItems.FirstOrDefault(item => item.Id == ItemId.Health_Potion);

                // Check if the player has a health pot
                if (healthPotItem != null)
                {
                    // Use the health pot
                    ObjectManager.Player.Spellbook.CastSpell(healthPotItem.SpellSlot);
                }

                // Reset the signal, allowing it to be called again.
                raisedArgs.Signal.Reset();

            }, signal => ObjectManager.Player.HealthPercent < (int) signal.Properties["HealthPercent"],
                DateTimeOffset.Now.AddMinutes(20), propertiesDictionary);'

Don't forget that you can get the signal from `Signal.Create` (It returns an instance of the `Signal` class), and go into the properties and change `HealthPercent`. A great use would be from a Menu.

Getting the signal from `Signal.Create` is easy.

	var signal = Signal.Create(..);


**Tip**: If you want your signal to not expire, but you need to use the properties dictionary, just pass in `DateTimeOffset.MaxValue`

## Enabling/Disabling Signals ##
Enabling and disabling signals are pretty easy. **Signals are automatically enabled when created.**

To enable a signal, call the `Enable` method.

	healthPotSignal.Enable();

And to disable it, call the `Disable` method.

	healthPotSignal.Enable();
