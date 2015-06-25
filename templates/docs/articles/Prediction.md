# Prediction #
----------
Prediction is used to predict the point of a unit in a given amount of time taking into account their current path, movement speed, dashes, your ping, etc.

## Prediction Types ##
For LeagueSharp projects, there are 3 types of prediction that we most commonly use.

- Movement Prediction
- Health Prediction
- Spell Prediction

Movement prediction simply mathematically predicts where a unit will be in an amount of time. Health prediction predicts the health of a unit, taking in account auto attacks, and should be typically used for minions only. Spell prediction predicts a location to cast a spell, and by using the movement prediction, will hit the unit after a delay, missile speed, and width/radius of the spell.


## Examples ##
<br />
**Movement Prediction**

    var movementPrediction = Movement.GetPrediction(ObjectManager.Player, 0.25f).UnitPosition;

This will get the position of the Player in 0.25 seconds (250 milliseconds).

**Health Prediction**

    var healthPred = Health.GetPrediction(Orbwalker.GetTarget() as Obj_AI_Base, 250);

This will get the predicted health of the unit after 250 milliseconds. 

**Spell Prediction**

    var castPosition = Movement.GetPrediction(TargetSelector.GetTarget(1000), 0.25f, 100, 1800).CastPosition;

You will almost never have to deal with getting the prediction manually, as the `Spell` class automatically gets the prediction when you cast the spell. This will get the cast position of a target with a delay of 0.25 seconds, a width of 100 units, and a speed of 1800 units/second.
