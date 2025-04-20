# OOP-submission
class Superhero:
    """Base class representing a generic superhero"""
    
    def __init__(self, name, secret_identity, powers, origin_story):
        self.name = name
        self.secret_identity = secret_identity  # Encapsulated attribute
        self._powers = powers                  # Protected attribute
        self.origin_story = origin_story
        self.health = 100                      # Default value
        self._is_retired = False              # Private attribute
    
    def use_power(self):
        """Use the superhero's main power"""
        if not self._is_retired:
            print(f"{self.name} uses {self._powers[0]}!")
        else:
            print(f"{self.name} is retired and can't use powers.")
    
    def take_damage(self, amount):
        """Reduce the superhero's health"""
        if not self._is_retired:
            self.health -= amount
            print(f"{self.name} takes {amount} damage! Health: {self.health}")
            if self.health <= 0:
                self.retire()
        else:
            print(f"{self.name} is already retired.")
    
    def heal(self, amount):
        """Restore health"""
        if not self._is_retired:
            self.health = min(100, self.health + amount)
            print(f"{self.name} heals {amount} points. Health: {self.health}")
        else:
            print("Retired heroes can't heal.")
    
    def retire(self):
        """Retire the superhero"""
        self._is_retired = True
        print(f"{self.name} has retired from hero work.")
    
    def reveal_secret_identity(self):
        """Reveal the secret identity"""
        print(f"{self.name}'s secret identity is {self.secret_identity}!")
    
    def __str__(self):
        return f"{self.name} - Powers: {', '.join(self._powers)} - Health: {self.health}"


class MutantHero(Superhero):
    """Subclass for mutant heroes with additional X-gene abilities"""
    
    def __init__(self, name, secret_identity, powers, origin_story, xgene_ability):
        super().__init__(name, secret_identity, powers, origin_story)
        self.xgene_ability = xgene_ability
        self._power_level = 10  # Mutants start with higher power
    
    def use_power(self):  # Polymorphism - overriding parent method
        if not self._is_retired:
            print(f"{self.name} activates their X-gene and uses {self._powers[0]} with power level {self._power_level}!")
        else:
            print(f"{self.name} is retired and can't use mutant powers.")
    
    def power_surge(self):
        """Special mutant ability to temporarily boost power"""
        if not self._is_retired:
            self._power_level += 5
            print(f"{self.name}'s power surges to {self._power_level}!")
        else:
            print("Retired mutants can't power surge.")


class TechHero(Superhero):
    """Subclass for tech-based heroes with upgradable gadgets"""
    
    def __init__(self, name, secret_identity, powers, origin_story, gadgets):
        super().__init__(name, secret_identity, powers, origin_story)
        self.gadgets = gadgets
        self._tech_level = 1
    
    def use_power(self):  # Polymorphism - overriding parent method
        if not self._is_retired:
            print(f"{self.name} activates {self.gadgets[0]} and uses {self._powers[0]}!")
        else:
            print(f"{self.name} is retired and their tech is deactivated.")
    
    def upgrade_tech(self):
        """Improve the hero's technology"""
        if not self._is_retired:
            self._tech_level += 1
            new_power = f"Tech-enhanced {self._powers[0]}"
            self._powers[0] = new_power
            print(f"{self.name}'s tech upgraded to level {self._tech_level}! New ability: {new_power}")
        else:
            print("Retired tech heroes can't upgrade.")


# Example usage
if __name__ == "__main__":
    # Create some heroes
    captain_marvel = Superhero(
        "Captain Kenya",
        "Liam Hudson",
        ["Super strength", "Flight", "Heat vision"],
        "Born with powers after cosmic radiation exposure"
    )
    
    storm = MutantHero(
        "Storm",
        "Nairobi Cail",
        ["Weather manipulation", "Flight"],
        "Descendant of ancient weather-worshipping priestesses",
        "Atmokinesis"
    )
    
    iron_engineer = TechHero(
        "Iron Engineer",
        "Tony Stone",
        ["Repulsor beams"],
        "Built a suit to escape captivity",
        ["Arc reactor", "Smart AI", "Nanotech suit"]
    )
    
    # Test the heroes
    print("--- Testing Captain Justice ---")
    print(captain_justice)
    captain_justice.use_power()
    captain_justice.take_damage(30)
    captain_justice.heal(10)
    captain_justice.reveal_secret_identity()
    
    print("\n--- Testing Storm ---")
    print(storm)
    storm.use_power()
    storm.power_surge()
    storm.use_power()
    storm.take_damage(120)  # This will retire her
    
    print("\n--- Testing Iron Engineer ---")
    print(iron_engineer)
    iron_engineer.use_power()
    iron_engineer.upgrade_tech()
    iron_engineer.use_power()
