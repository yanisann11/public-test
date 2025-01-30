# public-test
# Импорты
import numpy as np
import random
from enum import Enum

# 1. Генерация планеты
class Planet:
    def __init__(self, seed=42):
        self.seed = seed
        self.resources = {"металлы": 1e6, "вода": 5e6, "органика": 2e6}
        self.biomes = self.generate_biomes()
        
    def generate_biomes(self):
        # Процедурная генерация биомов (упрощённо)
        return np.random.choice(["лес", "пустыня", "океан", "горы"], size=(100, 100))

# 2. ДНК и существа
class DNA:
    def __init__(self, genes=None):
        self.genes = genes if genes else {"intelligence": 0.1, "curiosity": 0.5, "strength": 0.3}
        
class Creature:
    def __init__(self, dna=DNA()):
        self.dna = dna
        self.energy = 100
        self.skills = {"toolmaking": 0.0}

# 3. Нейросетевой интеллект
class NeuralBrain:
    def __init__(self, input_size=5, hidden_size=10):
        self.weights = np.random.randn(input_size, hidden_size)
        
    def forward(self, inputs):
        return np.dot(inputs, self.weights)

# 4. Цивилизация и эпохи
class Era(Enum):
    TRIBAL = 1
    INDUSTRIAL = 2
    DIGITAL = 3
    SPACE = 4

class Civilization:
    def __init__(self):
        self.tech_level = 0
        self.era = Era.TRIBAL
        self.inventions = []
        
    def evolve(self, planet):
        if self.tech_level > 10 and planet.resources["металлы"] > 1000:
            self.era = Era.INDUSTRIAL
            self.inventions.append("паровая_машина")

# 5. Космическая экспансия
class SpaceExpansion:
    def __init__(self, civ):
        self.civ = civ
        self.colonies = []
        
    def launch_colony_ship(self):
        if self.civ.tech_level >= 20:
            self.colonies.append("alpha_centauri")

# 6. Мета-эволюция
class MetaEvolution:
    def optimize_curiosity(self, civ):
        if civ.tech_level < 5:
            civ.dna.genes["curiosity"] *= 1.05

# 7. Глобальный симулятор
class GalaxySimulator:
    def __init__(self):
        self.planet = Planet()
        self.civ = Civilization()
        self.year = 0
        
    def run(self, years=1000):
        for _ in range(years):
            self.year += 1
            self.civ.evolve(self.planet)
            if self.year == 500:
                self.civ.era = Era.DIGITAL
            elif self.year == 800:
                SpaceExpansion(self.civ).launch_colony_ship()

# Запуск
sim = GalaxySimulator()
sim.run(1000)
print(f"Итоговая эра: {sim.civ.era}")
print(f"Изобретения: {sim.civ.inventions}")
