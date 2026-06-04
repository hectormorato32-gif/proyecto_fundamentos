import json
import os

ARCHIVO = "gastos.json"

def cargar():
    if os.path.exists(ARCHIVO):
        with open(ARCHIVO) as f:
            return json.load(f)
    return []

def guardar(gastos):
    with open(ARCHIVO, 'w') as f:
        json.dump(gastos, f)

def agregar(gastos):
    print("\n--- AGREGAR GASTO ---")
    monto = float(input("Monto: $"))
    categoria = input("Categoría: ")
    desc = input("Descripción: ")
    gastos.append({"monto": monto, "categoria": categoria, "desc": desc})
    guardar(gastos)

def ver(gastos):
    print("\n--- GASTOS ---")
    if not gastos:
        print("Sin gastos")
        return
    for i, g in enumerate(gastos, 1):
        print(f"{i}. {g['categoria']}: ${g['monto']} - {g['desc']}")

def total(gastos):
    print(f"\nTotal: ${sum(g['monto'] for g in gastos):.2f}\n")

def por_categoria(gastos):
    print("\n--- POR CATEGORÍA ---")
    cat = {}
    for g in gastos:
        c = g['categoria']
        cat[c] = cat.get(c, 0) + g['monto']
    for c, t in cat.items():
        print(f"{c}: ${t:.2f}")

gastos = cargar()
while True:
    print("\n1. Agregar  2. Ver  3. Total  4. Categoría  5. Salir")
    op = input("Opción: ")
    if op == "1": agregar(gastos)
    elif op == "2": ver(gastos)
    elif op == "3": total(gastos)
    elif op == "4": por_categoria(gastos)
    elif op == "5": break
