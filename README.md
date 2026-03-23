# Cafeteria
Proyecto cafeteria

print("Programa realizado por")
print("Bruno Macías Guerrero - 039901")
print("Salvador Flores Cazares - 39883")
print("Alonso Soto Barrera  - 39982")

class Pedido_Cafeteria():
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio):
        self.id_pedido = id_pedido
        self.tipo = tipo
        self.tamano = tamano
        self.azucar = azucar
        self.leche = leche
        self.precio = precio
        self.iva = self.precio * 0.16
        
    def mostrar_pedido(self):
        print(f"""Detalles del pedido:
ID: {self.id_pedido}
Tipo: {self.tipo}
Tamaño: {self.tamano}
Azúcar: {self.azucar}
Leche: {self.leche}
Precio base: {self.precio}""")
        
    def calcular_precio(self):
        return self.precio + self.iva


class Cafe_negro(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura):
        super().__init__(id_pedido, tipo, tamano, azucar, leche, precio)
        self.temperatura = temperatura
        
    def calcular_precio(self):
        if self.temperatura.lower() == "frio":
            extra = 5 
        else:
            extra = 0
        return self.precio + self.iva + extra



class Te_tissana(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura, hielos):
        super().__init__(id_pedido, tipo, tamano, azucar, leche, precio)
        self.temperatura = temperatura
        self.hielo = hielos
        
    def calcular_precio(self):
        if self.hielo == True:
            extra = 10
        else:
            extra = 0

        return self.precio + self.iva + extra

class Mocha_moka(Pedido_Cafeteria):
    def __init__(self, id_pedido, tipo, tamano, azucar, leche, precio, temperatura, aditivo):
        super().__init__(id_pedido, tipo, tamano, azucar, leche, precio)
        self.temperatura = temperatura
        self.aditivo = aditivo
        
    def calcular_precio(self):
        if self.aditivo.lower() in ["chocolate", "crema batida"]:
            extra = 20
        else:
            extra = 0
        return self.precio + self.iva + extra

pedido_1 = Cafe_negro(1, "Cafe", "Grande", 0, "sin leche", 80.00, "Caliente")
pedido_2 = Mocha_moka(2, "Cafe", "Mediano", 3, "Deslactosada", 94.00, "Frio", "Chocolate")
pedido_3 = Te_tissana(3, "Te", "Chico", 2, "sin leche", 76.00, "Frio", True)

pedido_total = [pedido_1, pedido_2, pedido_3]

for pedidos in pedido_total:
    pedidos.mostrar_pedido()
    print(f"Precio final: {pedidos.calcular_precio()}")


pedidos_usuario = []
contador_id = 4 

input("Presiona para continuar...")
import os
os.system("cls")   

while True:
    print("\n--- MENÚ ---")
    print("1. Cafe negro")
    print("2. Te")
    print("3. Mocha")
    print("4. Salir")

    opcion = int(input("Elige una opción: "))

    if opcion == 4:
        break

    tamano = input("Tamaño (Chico/Mediano/Grande): ")
    azucar = int(input("Cantidad de azúcar: "))
    leche = input("¿Tiene leche? (si/no): ")

    precio_base = 50  # base general

    if opcion == 1:
        temperatura = input("Caliente o Frio: ")
        pedido = Cafe_negro(contador_id, "Cafe", tamano, azucar, leche, precio_base, temperatura)

    elif opcion == 2:
        temperatura = input("Caliente o Frio: ")
        hielo = input("¿Deseas hielo? (si/no): ").lower() == "si"
        pedido = Te_tissana(contador_id, "Te", tamano, azucar, leche, precio_base, temperatura, hielo)

    elif opcion == 3:
        temperatura = input("Caliente o Frio: ")
        aditivo = input("Chocolate / crema batida / ninguno: ")
        pedido = Mocha_moka(contador_id, "Mocha", tamano, azucar, leche, precio_base, temperatura, aditivo)

    else:
        print("Opción inválida")
        continue

    pedidos_usuario.append(pedido)
    contador_id += 1


print("\n--- PEDIDOS REALIZADOS ---")
for pedido in pedidos_usuario:
    print("-------------------")
    pedido.mostrar_pedido()
    print(f"Precio final: ${pedido.calcular_precio()}")
