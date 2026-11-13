from random import randint  # Para elegir números al azar (enemigo y quién ataca primero)


# Clase base (padre): define lo que tienen en común todos los personajes.
class Hero():
    # Constructor: se ejecuta al crear un personaje y guarda sus características.
    def __init__(self, name, health, armor, power):
        self.name = name      # Nombre del personaje
        self.health = health  # Nivel de vida
        self.armor = armor    # Armadura: absorbe el daño antes que la vida
        self.power = power    # Fuerza de impacto (daño que causa al golpear)
        self.new = True       # Indica si es la primera vez que aparece en escena

    # Muestra en pantalla la vida y la armadura actuales del personaje
    def print_info(self):
        print('Nivel de vida:', self.health)
        print('Clase de armadura:', self.armor)

    # Comprueba si el personaje sigue vivo.
    # Devuelve True si su vida es mayor que 0, y False en caso contrario.
    def check_alive(self):
        if self.health > 0:
            return True
        else:
            return False

    # Golpe: el personaje actual (self) daña a otro (enemy).
    # Este método solo calcula el daño; no imprime nada.
    def strike(self, enemy):
        # Primero el golpe reduce la armadura del enemigo
        enemy.armor -= self.power
        # Si la armadura quedó en negativo, el daño sobrante pasa a la vida
        # (se suma porque armor es negativo) y la armadura queda en 0
        if enemy.armor < 0:
            enemy.health += enemy.armor
            enemy.armor = 0


# Clase hija: Warrior hereda de Hero, así que ya tiene __init__, print_info,
# check_alive y strike. Aquí solo agregamos lo que es propio del guerrero.
class Warrior(Hero):
    # Mensaje de aparición. Cambia según sea la primera vez o no.
    def hello(self):
        if self.new:
            print('-> ¡NUEVO HÉROE! Un guerrero habilidoso aparece desde las profundidades del bosque', self.name)
            self.new = False  # Ya no es nuevo: la próxima vez dirá "aparece de nuevo"
        else:
            print('El marcial', self.name, 'aparece de nuevo')

    # Método para mostrar en pantalla una descripción de texto del ataque
    # y el resultado del combate para ambos personajes.
    def attack(self, enemy):
        print(self.name, 'se abalanza sin miedo en', enemy.name)
        print('El resultado de la lucha para', self.name)
        self.print_info()
        print('El resultado de la lucha para', enemy.name)
        enemy.print_info()


# Clase hija: Dragon también hereda de Hero.
# Tiene los mismos métodos (hello, attack) que Warrior pero con textos distintos.
# Esto es polimorfismo: el mismo nombre de método se comporta diferente según la clase.
class Dragon(Hero):
    def hello(self):
        if self.new:
            print('-> ¡NUEVO HÉROE! El dragón feroz', self.name, ' desciende desde el cielo')
            self.new = False
        else:
            print('Una vez más el dragón furioso', self.name, 'aparece ante nosotros')

    def attack(self, enemy):
        print(self.name, 'dirige un torrente de fuego mortal contra', enemy.name)
        print('El resultado de la lucha para', self.name)
        self.print_info()
        print('El resultado de la lucha para', enemy.name)
        enemy.print_info()


# ---------- PROGRAMA PRINCIPAL ----------

# Creamos al jugador: un objeto de la clase Warrior
knight = Warrior('Richard', 50, 25, 20)
print('Salve a ti, buen caballero', knight.name)
print('Te encuentras a la entrada del bosque lleno de peligros mortales. ¿Estás listo para adentrarte y luchar contra los enemigos (si/no)?')

# input() espera a que el usuario escriba una respuesta
answer = input()
if answer == 'si':
    play = True  # La variable play controla si el juego continúa
    print('\n***¡Que comience la pelea!*** \n')
else:
    play = False  # Si no responde "si", el ciclo principal no se ejecutará

# Lista con los enemigos: mezcla objetos Warrior y Dragon.
# Al heredar de Hero, todos se pueden tratar de la misma forma.
enemies = list()
enemies.append(Warrior('Peter', 15, 0, 10))
enemies.append(Warrior('Sergio', 10, 15, 5))
enemies.append(Dragon('Drogon', 1, 25, 60))
enemies.append(Dragon('Viserion', 1, 10, 30))

# Ciclo principal: cada vuelta es un encuentro con un enemigo
while play:
    # Elegimos un enemigo al azar de la lista.
    # Usamos len(enemies) como límite porque la lista se achica al derrotar enemigos.
    enemy = enemies[randint(0, len(enemies) - 1)]
    enemy.hello()       # Mensaje de aparición (según su clase)
    enemy.print_info()  # Muestra su vida y armadura

    # El jugador decide si pelea o no
    is_attack = input('¿Unirse a la pelea (si/no)?')
    if is_attack == 'si':
        # Se decide al azar quién golpea: fighters[0] ataca, fighters[1] defiende
        if randint(0, 1) == 1:
            fighters = [knight, enemy]
        else:
            fighters = [enemy, knight]
        fighters[0].strike(fighters[1])   # Calcula el daño (armadura y vida)
        fighters[0].attack(fighters[1])   # Muestra el texto del ataque y el resultado
    print('---')

    # Si el enemigo murió, lo eliminamos de la lista
    if enemy.check_alive() == False:
        print(enemy.name, 'murió bajo la mano de', knight.name, '\n')
        enemies.remove(enemy)

    # Condiciones de fin del juego:
    # 1) El caballero murió
    if knight.check_alive() == False:
        print('El caballero valiente', knight.name, 'murió en la batalla con los enemigos')
        play = False
    # 2) Ya no quedan enemigos
    if len(enemies) == 0:
        print('¡El valiente Caballero', knight.name, 'derrotó a todos los enemigos!')
        play = False

print('Este es el final de este cuento mágico')
