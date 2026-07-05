# Attributes

*Attributes* are the most important feature in this system. They define values that expresses the characteristics of an entity (anything "alive", NPC, player, zombies, animals...), like its health. Here's the basic layout of it:

```cpp
struct Attribute
{
    std::string id;
    float value = 1;
};
```

*Note: I included an `id` field in order to it easier to locate attributes inside the game.*



Two fields, `id` for its name, `value` for the actual value of the attribute. Pretty simple, right?



## Needs

In some cases, you'll want an attribute to be important to an entity, so that it'd have to care about it and make sure the value is closest possible to its ideal. That's called a *Need* (couldn't think in a better name).

Since an entity may have multiple needs, it must have a way of deciding which one has the higher priority in the current moment. That priority is calculated by how far the value of the attribute is from its ideal, and how important is that attribute. Setting an importance to each need is recommended because a `hydration` (thirst) need obviously has less priority than making sure your `health` is in good conditions. Some needs decrease their `value` naturally with time, like the cited above `hydration`, plus others including `satiation` (hunger). Given that definition, we could expand the original `Attribute` struct to:

```cpp
```cpp
struct Attribute
{
    std::string id;
    float value = 1;
    
    bool is_a_need = false;
    float importance = 1;
    float ideal = 1;
    float variation = 0;
};


inline float attribute_calculate_priority(const Attribute& attribute)
{
    return attribute.is_a_need ? attribute.importance * abs(attribute.ideal - attribute.value) : 0;
}
```
```

*Note: The `abs` (stands for "absolute") function forces a value to be positive. Expliciting this here just to make sure no confusions are made.*

*Note: In usual circunstances, I'd use a polymorphism based approach to implement the above logic. But since the game mainly or fully uses procedural programming, I'll try to adapt it to procedural as much as I can. However, I'm not the most experienced with raw procedural programming, so it may not be the best way of implementing it. Also, note the use of C++ features like initialization of fields inside the declaration (`float value = 1`), `std::string` and, more below, `std::vector`. I'm using these for simplicity reasons, and because I've seen that you use them too inside the engine.*



If the attribute isn't a need, there would have no sense on having a priority for it, so if that's the case, `0` is returned. As said above, the distant the `value` is from its `ideal`, the higher the priority.

The field `variation` is how `value` is changed over time. Negative values decrease it, positive ones increase.



## Suggestions

- The normalized nature of `Attribute::value` (from 0 to 1, 0% to 100%) can cause some trouble when it's needed to display the attribute using a specific metric system. When you need that, multiplying the value by a reference metric value will solve it. For example, for `temperature`, you could want do display it using the Celsius format. To do that, we could say that 100% equals to the n


