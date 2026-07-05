- Tolerance mechanics: How much the value can be far from its ideal without increasing the priority. Two fields (float), `below_tolerance` and `above_tolerance`, tolerance for when the value is below and above its ideal, respectively.

- Clamping mechanics:
  
  - Being able to allow the value to be higher or lower than its ideal. (bool) `ideal_is_min` (`true`: can't go lower than `ideal`) and `ideal_is_max`.
  
  - Define custom values forcing the attribute value to be between these. (float) `min` and `max`. If `min > ideal`, it'll be ignored. If `max < ideal`, it'll be ignored. `ideal_is_min` and `ideal_is_max` have priority over these, that is, if `ideal_is_min == true`, `min` will be ignored. Same for `ideal_is_max` and `max`.

- Finish effect system.

- Start Opportunity system.


