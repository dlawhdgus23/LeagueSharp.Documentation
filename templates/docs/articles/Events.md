**Events**
--------
Events are user actions such as key press, clicks, mouse movements, or some occurrence such as system generated notifications. Applications need to respond to events when they occur. 
To simply, an *event* is when something happens in program that requires some action to be taken. Every time you click your mouse you **rise** and mouse click **Event**. Depending on where you click it is *handled* differently.  
*Events* are tied to *Delegated* and talking about one without other is practically pointless. 
You can think of Delegate as a function to be executed when an event it's tied to is *raised*.
>**Note**: In programing it's said that delegate is subscribed to an event or is listening on event.



        using System;
    
        namespace EventExample
        {
             public class Online Shopping Cart
              {
                Cart My Cart = new Cart();
                button addToCart = new button {name="add to cart"}; /*this is done automatically but still*/
                button checkOut = new button {name ="checkout"};
                add To Cart.OnClick=ButtonClicked; //ButtonClicked subbed
                checkOut.OnClick=OnButtonClied; /*Notice it's same delegate. You could use two but that is the easy way. Let's do it hard way :D*/
          public static void ButtonClicked (object sender, EventArgs args)
                {
           var sender = (uibutton) sender;
           if(sender.Name="add to cart"))
                MyCart.Add(sender.Item);
           else if (sender.Name="checkout")
                My Cart.Checkout();
           else
               Console.WriteLine("Bad event trigger");//I made this up FYI     
                }
             }
       }
            
            
There are more ways to do this ofc. One would be to declare one more Button liked delegate like UnButton liked Checkout. You could also define a delegate that would act as method pointer and call the method as needed by event rises. More about that in delegatet section :)
##LSharp example##
For the example we will use **LSharp** code and syntax.

        using System;
        using System.Collections.Generic;
        using System.IO;
        using LeagueSharp;
        using LeagueSharp.Common;
        using LeagueSharp.Sandbox;
        
        namespace 
        {
           internal class Program
           {
             static Menu _main;
             //spells and stuff declaration here
             
             public static void Main(string[] args)
                 {
            Custom Events.Game.On Game Load += Game_OnGameLoad; //triggers when game loads
                  }
            static void Game_OnLoad()
               {
                  _main = new Menu ("AssemblyName","menuname",true);
                  _main.Add MainMenu();
                  //other menus and spell definitions
                  //...
                  //...
                 Game.OnUpdate=OnUpdate; /*triggered by every change in game and orbwalker modes*/
                }
            static void OnUpdate()
                {
            /*here go the orbwalker modes and custom methods you want to invoke on game update such as kill count checks, other score checks, anything you can think of actually. There are many events that already exist.
                }
          }
  }

Full event list will be added soon :)
          
         



