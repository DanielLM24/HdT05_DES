# -*- coding: cp1252 -*-
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
CANTIDAD_PROCESOS = 25

def source(env, cantidad, intervalo):
    for i in range(cantidad):
        instrucciones = random.randint(1,10)
        memoria = random.randint(1,10)
        p = env.process(proceso(env, 'Proceso %d' % i, instrucciones, memoria))
        t = random.expovariate(1.0/intervalo)
        yield env.timeout(t)

def proceso(env, nombre, instrucciones, memoria):
    arrive = env.now
    print('%7.4f %s: llega' % (arrive, nombre))
    global totalTime

    yield ram.get(memoria)
    print('Memoria obtenida %d' % memoria)

    yield env.timeout(5)

    yield ram.put(memoria)

    print ('salida')
   
random.seed(RANDOM_SEED)
env = simpy.Environment()
totalTime = 0
env = simpy.Environment()
random.seed(RANDOM_SEED)
cpu = simpy.Resource(env,1)
ram = simpy.Container(env, CAPACIDAD_RAM, init=0)
env.process(source(env,10,INTERVALO))
env.run()

x = raw_input("Espera")
