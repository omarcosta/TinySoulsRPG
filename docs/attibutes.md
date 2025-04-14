# Atributes progress

## Atributes progress

| Attribute     | Main Effects                                        |
|---------------|-----------------------------------------------------|
| Vigor         | Increases HP (health)                               |
| Mind          | Increases MP (mana) and resistance to magic attacks |
| Endurance     | Increases Stamina and resistance to basic attacks   |
| Strength      | Increases physical attack damage                    |
| Intelligence  | Increases magic damage                              |
| Luck          | Improves item drop rate and overall in-game luck    |

## Atributes scalling

| Attribute     | Affected Stat  | Formula                                 | At 10 Points | At 20 Points   |
|---------------|----------------|-----------------------------------------|--------------|----------------|
| Vigor      | Max HP       | `hp_max = base.hp * (1 + 0.04 * (vigor - 1))`           | 1360 | 1760   |
| Mind       | Max MP       | `mp_max = base.mp * (1 + 0.05 * (mind - 1))`            | 145  | 195    |
| Endurance  | Max Stamina  | `stamina = base.stamina * (1 + 0.03 * (endurance - 1))` | 127  | 157    |
| Strength      | Physical Damage   | `base.damage = 10 * (1 + 0.06 * (strength - 1))`           | 15.4           | 21.4           |
| Intelligence  | Magic Damage      | `base.magic = 10 * (1 + 0.07 * (intelligence - 1))`        | 16.3           | 23.3           |
| Luck          | Drop Rate         | `base.rate = 1 * (1 + 0.08 * (luck - 1))`              | 1.72           | 2.52           |

### Real formula

`Player.current.hp_max      = Player.base.hp      * (1 + 0.04 * (Player.attributes.vigor        - 1))`
`Player.current.mp_max      = Player.base.mp      * (1 + 0.05 * (Player.attributes.mind         - 1 ))`
`Player.current.stamina_max = Player.base.stamina * (1 + 0.03 * (Player.attributes.endurance    - 1))`
`Player.current.damage      = Player.base.damage  * (1 + 0.06 * (Player.attributes.strength     - 1))`
`Player.current.magic       = Player.base.magic   * (1 + 0.07 * (Player.attributes.intelligence - 1))`
`Player.current.rate        = Player.base.rate    * (1 + 0.08 * (Player.attributes.luck         - 1))` 

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