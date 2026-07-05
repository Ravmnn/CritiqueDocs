# Attributes

*Attributes* are the most important feature in this system. They define values that expresses the characteristics of an entity (anything "alive", NPC, player, zombies, animals...), like its health. Here's the basic layout of it:

```cpp
struct Attribute
{
    std::string id;
    float value = 1;
};
```

<small>*Note: I included an `id` field in order to it easier to locate attributes inside the game.*</small>

Two fields, `id` for its name, `value` for the actual value of the attribute. Pretty simple, right?

## Needs

Ocasionally, you'll want an attribute to be important to an entity, so that it'd have to care about it and make sure the value is closest possible to its ideal. That's called a *Need*.

Since an entity may have multiple needs, it must have a way of deciding which one has the higher priority in the current moment. That priority is calculated by how far the value of the attribute is from its ideal, and how important is that attribute. Setting an importance to each need is recommended because a `hydration` (thirst) need obviously has less priority than making sure your `health` is in good conditions. Some needs decrease their `value` naturally with time, like the cited above `hydration`, plus others including `satiation` (hunger). Finally, it's important a need to be able to tolerate certain amount of disparity from its ideal before increasing the priority for it. Given that definition, we could expand the original `Attribute` struct to:

```cpp
struct Attribute
{
    std::string id;
    float value = 1;

    bool is_a_need = false;
    float importance = 1;
    float ideal = 1;
    float variation = 0;
    float below_tolerance = 0;
    float above_tolerance = 0;
};


inline float attribute_calculate_priority(const Attribute& attribute)
{
    if (attribute.value >= attribute.ideal - attribute.below_tolerance && )

    const float ideal_reference = attribute.value < ideal ?
        attribute.ideal - abs(attribute.below_tolerance) :
        attribute.ideal + abs(attribute.above_tolerance);

    return attribute.is_a_need ? attribute.importance * abs(ideal_reference - attribute.value) : 0;
}
```

<small>*Note: The `abs` (stands for "absolute") function forces a value to be positive. Expliciting this here just to make sure no confusions are made.*</small>

<small>*Note: In usual circunstances, I'd use a polymorphism based approach to implement the above logic. But since the game mainly or fully uses procedural programming, I'll try to adapt it to procedural as much as I can. However, I'm not the most experienced with raw procedural programming, so it may not be the best way of implementing it. Also, note the use of C++ features like initialization of fields inside the declaration (`float value = 1`), `std::string` and, more below, `std::vector`. I'm using these for simplicity reasons, and because I've seen that you use them too inside the engine.*</small>

If the attribute isn't a need, there would have no sense on having a priority for it, so if that's the case, `0` is returned. As said above, the distant the `value` is from its `ideal`, the higher the priority.

The field `variation` is how `value` is changed over time. Negative values decrease it, positive ones increase.

`below_tolerance` and `above_tolerance` specify how much `value` can go below or above `ideal` before increasing priority.

In some cases there's no sense in a need's `value` to be negative or above its `ideal` value. That's the case of a `health` need. So another important addition to our current attribute struct would be clamping features:

```cpp
struct Attribute
{
    std::string id;
    float value = 1;

    bool is_a_need = false;
    float importance = 1;
    float ideal = 1;
    float variation = 0;
    

    bool ideal_is_min = false;
    bool ideal_is_max = false;
    std::optional<float> min;
    std::optional<float> max; 
};
```

<small>*Note: `std::optional` is a very useful C++ class that makes a value optional, so it can or not have a value. In raw C, the only way of doing it would be using pointers, or creating a separated boolean that determines whether the specific object has or not a value.*</small>

`ideal_is_min` and `ideal_is_max` (when `false`) determines whether `value` can go below or above `ideal`, respectively. `min` and `max` are similar, but instead of using `ideal` as the limiter, it allows you to choose a custom value. Note that if `min > ideal` or `max < ideal`, the respective field should be ignored. `ideal_is_min` and `ideal_is_max` have priority over `min` and `max`.
