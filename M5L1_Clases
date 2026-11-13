from random import randint
from time import sleep


class Hero():
    """
    Clase Hero (Héroe):
    Es el "molde" para crear personajes de combate. Cada objeto creado a partir
    de esta clase representa a un héroe con sus propias características
    (nombre, vida, armadura, fuerza y arma) y con las acciones que puede
    realizar (mostrar su información y atacar a un enemigo).
    """

    # Constructor: se ejecuta automáticamente cada vez que se crea un nuevo
    # héroe, por ejemplo: Hero('Richard', 50, 25, 20, 'espada').
    # Recibe los valores iniciales y los guarda como atributos del objeto.
    # "self" se refiere al objeto que se está creando.
    def __init__(self, name, health, armor, power, weapon):
        self.name = name      # Nombre del héroe
        self.health = health  # Nivel de vida (si llega a 0 o menos, pierde)
        self.armor = armor    # Clase de armadura (absorbe el daño antes que la vida)
        self.power = power    # Fuerza de impacto (daño que causa al atacar)
        self.weapon = weapon  # Arma que utiliza

    # Método que muestra en pantalla las características del personaje:
    def print_info(self):
        print('Saluda al héroe ->', self.name)
        print('Nivel de vida:', self.health)
        print('Clase de armadura:', self.armor)
        print('Fuerza de impacto:', self.power)
        print('Arma:', self.weapon, '\n')

    # Método de ataque: el héroe actual (self) golpea a otro héroe (enemy).
    def strike(self, enemy):
        print('-> ¡ATACA! ')
        print(self.name, 'attacks', enemy.name, 'using', self.weapon, '\n')
        # Primero el golpe reduce la armadura del enemigo
        enemy.armor -= self.power
        # Si la armadura queda en negativo, el daño sobrante pasa a la vida
        # (se suma porque la armadura es un número negativo) y la armadura queda en 0
        if enemy.armor < 0:
            enemy.health += enemy.armor
            enemy.armor = 0
        print(enemy.name, 'sometido.')
        print('La clase de armadura bajó a', enemy.armor)
        print('El nivel de vida bajó a', enemy.health, '\n')


# Creación de los objetos (instancias) de la clase Hero.
# Cada línea llama al constructor __init__ con sus propios valores:
knight = Hero('Richard', 50, 25, 20, 'espada')
rascal = Hero('Helen', 100, 10, 15, 'arco')

# Mostramos la información inicial de cada héroe
knight.print_info()
rascal.print_info()

print('¡Que comience la batalla!')

# Ciclo principal del juego: se repite mientras play sea True
play = True
while play:
    # Se elige al azar quién ataca primero en este turno:
    # fighters[0] es el atacante y fighters[1] es el defensor
    if randint(0, 1) == 1:
        fighters = [knight, rascal]
    else:
        fighters = [rascal, knight]
    fighters[0].strike(fighters[1])
    # Si el defensor se queda sin vida, termina la batalla
    if fighters[1].health <= 0:
        play = False
        print(fighters[1].name, 'cayó en una dura batalla.')
    sleep(1)  # Pausa de 1 segundo entre turnos para poder leer el combate
