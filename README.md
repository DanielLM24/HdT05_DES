"""
Universidad del Valle de Guatemala
Algoritmos y Estructuras de Datos
Santiago González 13263
Daniel Lara Moir 13424
CPU.py
DES para sistema operativo. Simula el comportamiento del procesador con la llegada
y ejecución de instrucciones.
"""
import itertools
import random

import simpy
CAPACIDAD_RAM = 100
RANDOM_SEED = 23
INTERVALO = 10.0

def source(env, cantidad, intervalo):
    for i in range(cantidad):
        instrucciones = randint(1,10)
        memoria = randint(1,10)
        #p = proceso(env, instrucciones, memoria)
        t = random.expovariate(1.0/intervalo)
        yield env.timeout(t)

    


totalTime = 0
env = simpy.Environment()
random.seed(RANDOM_SEED)
cpu = simpy.Resource(env,1)
ram = simpy.Container(env, CAPACIDAD_RAM, init=0)
env.run()

x = input("Espera")
