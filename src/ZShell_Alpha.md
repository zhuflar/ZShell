# ZShell - Versión Alpha
import ctypes
import subprocess
import os
import sys

def es_admin():
    try:
        return ctypes.windll.shell32.IsUserAnAdmin()
    except:
        return False

def elevar():
    if not es_admin():
        script = os.path.abspath(sys.argv[0])
        ctypes.windll.shell32.ShellExecuteW(None, "runas", sys.executable, f'"{script}"', None, 1)
        sys.exit()

def bienvenida():
    print("=" * 60)
    print("              Bienvenido a ZShell              ")
    print("=" * 60)
    print("\nZShell es una herramienta multifuncional para tareas IT con permisos de administrador.")
    print("Esta versión ALPHA incluye algunos comandos básicos del sistema.")
    print("\nÚselo con responsabilidad. La versión completa incluye más categorías y funciones.\n")

def mostrar_menu():
    print("Menú:")
    print("1. Mostrar información de red (ipconfig)")
    print("2. Salir")

def ejecutar_comando(opcion):
    if opcion == "1":
        subprocess.run("ipconfig", shell=True)
    elif opcion == "2":
        print("¡Hasta pronto!")
        sys.exit()
    else:
        print("Opción no válida.")

if __name__ == "__main__":
    elevar()
    bienvenida()
    while True:
        mostrar_menu()
        eleccion = input("\nSelecciona una opción: ")
        ejecutar_comando(eleccion)
