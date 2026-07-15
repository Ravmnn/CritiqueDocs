# Needs

---

## Blood Level

- Effects:
  
  - When < 60%:
    
    - Causes weak [Nausea](./States.md#nausea)
    
    - Speed decreases proportionally
  
  - When < 35%:
    
    - Causes intense Nausea
  
  - When 0%:
    
    - Death

## 

## Food

- Effects:
  
  - When < 50%:
    
    - Stamina recovers more slowly, proportionally
    
    - Speed decreases, proportionally
  
  - When < 15%:
    
    - Blood Level decreases, proportionally

## 

## Water

- Effects:
  
  - When < 70%:
    
    - Stamina recovers more slowly, proportionally
  
  - When < 25%:
    
    - Blood Level decreases, proportionally
  
  - When 0%:
    
    - Death

## 

## Stamina

- Effects:
  
  - When < 30%:
    
    - Entity running speed starts to slightly decrease towards the walk speed, proportionally to how close to 0% stamina is.
- Decreases:
  - When the entity is running
- Increases:
  - When the entity is walking
  - When the entity is idle, 20% more than when it's walking





## Energy

- Effects:
  
  - When < 60%:
    
    - Stamina decreases faster and recovers slower, proportionally
  
  - When < 35%:
    
    - Stamina maximum value starts to decrease towards 70%, proportionally
  - When 0%:
    - The entity faints to recover it, since it recovers only by sleeping.
- Decreases:
  - Naturally when idle, slow
  - When walking, 5% more than when idle
  - When running, 15% more than when idle
- Increases:
  - Sleeping
