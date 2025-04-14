# Atributes progress

## Atributes progress

| Attribute     | Main Effects                                        |
|---------------|-----------------------------------------------------|
| Vigor         | Increases HP (health)                               |
| Mind          | Increases MP (mana) and resistance to magic attacks |
| Endurance     | Increases Stamina and resistance to basic attacks   |
| Strength      | Increases physical attack damage                    |
| Intelligence  | Increases magic damage                              |
| Luck          | Improves item drop rate and overall in-game luck (Ex: critical chance)   |

## Atributes scalling

| Attribute     | Affected Stat     | Formula                                               |
|---------------|-------------------|-------------------------------------------------------|
| Vigor         | Max HP            | `hp_max = base.hp * (1 + ASF * (vigor - 1))`          |
| Mind          | Max MP            | `mp_max = base.mp * (1 + ASF * (mind - 1))`           |
| Endurance     | Max Stamina       | `stamina = base.stamina * (1 + ASF * (endurance - 1))`|
| Strength      | Physical Damage   | `damage = base.damage * (1 + ASF * (strength - 1))`   |
| Intelligence  | Magic Damage      | `magic = base.magic * (1 + ASF * (intelligence - 1))` |
| Luck          | Drop Rate         | `rate = base.rate * (1 + ASF * (luck - 1))`           |

### 1. Attribute Scale Factor (ASF)

| Attribute     | ASF     | Base Stats (ALv.1)  | Max Stats (ALv.99)   |
|---------------|---------|---------------------|----------------------|
| Vigor         | 0.0578  |HP: 300              | HP: 2000 |
| Mind          | 0.0510  |MP: 50               | MP: 300  |
| Endurance     | 0.0306  |Stamina: 100         | Stamina: 400|
| Strength      | 0.0910  |Damage: 10           | Damage: 100 |
| Intelligence  | 0.0910  |Magic: 10            | Magic: 100  |
| Luck          | 0.0205  |Rate: 1 (100%)       | Rate: 3 (300%)|

ALv.: Attribute Level (1 to 99)

### 2. Real formula

Player.current.hp_max: `Player.base.hp * (1 + Player.ASF.vigor * (Player.attributes.vigor        - 1))`
Player.current.mp_max: `Player.base.mp * (1 + Player.ASF.mind * (Player.attributes.mind         - 1 ))`
Player.current.stamina_max: `Player.base.stamina * (1 + Player.ASF.endurance * (Player.attributes.endurance    - 1))`
Player.current.damage: `Player.base.damage  * (1 + Player.ASF.strength * (Player.attributes.strength     - 1))`
Player.current.magic: `Player.base.magic * (1 + Player.ASF.intelligence * (Player.attributes.intelligence - 1))`
Player.current.rate: `Player.base.rate * (1 + Player.ASF.luck * (Player.attributes.luck - 1))`

---
## Pontos de melhoria

### Optional Improvements (no need, but good to consider later)

#### Soft Cap (Diminishing Returns)
After a certain threshold (like 30 or 40), reduce the scale factor to simulate diminishing returns:

```python
if stat > 30:
    scale *= 0.5
```

#### Flat Bonus Additions
For small flavor bonuses, you could add a flat amount alongside the multiplier, example:

```python
HP = 1000 * (1 + 0.04 * (Vigor - 1)) + Vigor * 2
```

#### Dependencies entre atributos
Dependencies entre atributos
For example: magic damage could scale 90% with Intelligence and 10% with Luck.