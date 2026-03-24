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
        
    def mostrar_pedido(self):
        print(f"""Detalles del pedido:
ID: {self.id_pedido}
Tipo: {self.tipo}
Tamaño: {self.tamano}
Azúcar: {self.azucar}
Leche: {self.leche}
Precio base: {self.precio}""")
        
    def calcular_precio(self):
        iva = self.precio * 0.16
        return self.precio + iva


def precio_por_tamano(tamano):
    tamano = tamano.lower()
    if tamano == "chico":
        return 50
    elif tamano == "mediano":
        return 65
    elif tamano == "grande":
        return 80
    else:
        return 50


class Frappe(Pedido_Cafeteria):
    def __init__(self, id_pedido, tamano, azucar, leche, precio, aditivo_extra):
        super().__init__(id_pedido, "Frappe", tamano, azucar, leche, precio)
        self.aditivo_extra = aditivo_extra
        
    def calcular_precio(self):
        if self.aditivo_extra.lower() == "si":
            extra = 20
        else:
            extra = 0

        subtotal = self.precio + extra
        iva = subtotal * 0.16
        return subtotal + iva


class Te_tissana(Pedido_Cafeteria):
    def __init__(self, id_pedido, tamano, azucar, leche, precio, temperatura, hielo):
        super().__init__(id_pedido, "Te", tamano, azucar, leche, precio)
        self.temperatura = temperatura
        self.hielo = hielo
        
    def calcular_precio(self):
        if self.hielo:
            extra = 10
        else:
            extra = 0

        subtotal = self.precio + extra
        iva = subtotal * 0.16
        return subtotal + iva


class Mocha_moka(Pedido_Cafeteria):
    def __init__(self, id_pedido, tamano, azucar, leche, precio, temperatura, aditivo):
        super().__init__(id_pedido, "Mocha", tamano, azucar, leche, precio)
        self.temperatura = temperatura
        self.aditivo = aditivo
        
    def calcular_precio(self):
        if self.aditivo.lower() == "chocolate" or self.aditivo.lower() == "crema batida":
            extra = 20
        else:
            extra = 0

        subtotal = self.precio + extra
        iva = subtotal * 0.16
        return subtotal + iva



pedidos_usuario = [None] * 100
indice = 0
contador_id = 1 

while True:
    print("\n--- MENÚ ---")
    print("1. Frappe")
    print("2. Té")
    print("3. Mocha")
    print("4. Salir")

    opcion = int(input("Elige una opción: "))

    if opcion == 4:
        break

    tamano = input("Tamaño (Chico/Mediano/Grande): ")
    precio_base = precio_por_tamano(tamano)

    azucar = int(input("Cantidad de azúcar: "))
    leche = input("Tipo de leche: ")

    if opcion == 1:
        aditivo_extra = input("¿Deseas aditivo extra? (si/no): ")
        pedido = Frappe(contador_id, tamano, azucar, leche, precio_base, aditivo_extra)

    elif opcion == 2:
        temperatura = input("Caliente o Frío: ")
        hielo = input("¿Deseas hielo? (si/no): ")
        if hielo.lower() == "si":
            hielo = True
        else:
            hielo = False

        pedido = Te_tissana(contador_id, tamano, azucar, leche, precio_base, temperatura, hielo)

    elif opcion == 3:
        temperatura = input("Caliente o Frío: ")
        aditivo = input("Chocolate / crema batida / ninguno: ")
        pedido = Mocha_moka(contador_id, tamano, azucar, leche, precio_base, temperatura, aditivo)

    else:
        print("Opción inválida")
        continue


    pedidos_usuario[indice] = pedido
    indice = indice + 1
    contador_id = contador_id + 1



print("\n--- PEDIDOS REALIZADOS ---")
precio_final = 0

for cont in range(indice):
    print("-------------------")
    pedidos_usuario[cont].mostrar_pedido()
    total = pedidos_usuario[cont].calcular_precio()
    print(f"Precio final: ${total:.2f}")
    
    precio_final = precio_final + total

print(f"\nEl total a pagar es: ${precio_final:.2f}")
