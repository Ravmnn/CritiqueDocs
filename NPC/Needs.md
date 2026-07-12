# Needs

Using the 0% - 100% value range approach, where the entity (player, animal, NPC, zombie, etc) will try to keep its need value the highest possible.

There should have two kinds of modifications in a need's value. The first one doesn't affect the real value of a need, but rather it influentiates to the final calculation of it; it's called a "final" modification. The other one modifies the original need value; it's called "original". Original modifications happen every amount of game ticks, while final modifications always apply a constant change to the final calculation, like -20% or +5%.

Using the following format:

- Other needs: [This Way]()

- Need properties and calculations: `this way`

---

## Blood Level

- Type: liquid

- Effects:
  
  - When < 85%:
    
    - Causes [Nausea](./States.md#nausea)

## Body Temperature

- Type: temperature

- Negative: true

- Ideal: custom

- Effects: custom
