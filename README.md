[README.md](https://github.com/user-attachments/files/33468967/README.md)
# Control ambiental de un invernadero

**Integrantes:**
- Gabriel Diaz
- Saray Silva
- Paola Sanchez

---

## ¿De qué trata?

Este es el segundo parcial. Hicimos un programa que controla la temperatura y la humedad de un cultivo en un invernadero. Pide las lecturas una por una y con cada una decide si el cultivo está bien, si hay que corregir algo o si hay una emergencia. Al final muestra un resumen con los mínimos, máximos, promedios y las secuencias de datos.

## Rangos que usa

| Variable | Rango óptimo | Es crítico si está fuera de |
| --- | --- | --- |
| Temperatura | 18 a 26 °C | 12 a 32 °C |
| Humedad | 60 a 80 % | 40 a 90 % |

Además, el sensor solo acepta temperaturas entre -10 y 60 °C y humedad entre 0 y 100 %. Si el dato queda fuera de eso, el programa muestra "Dato inválido" y vuelve a pedir la lectura (no se cuenta). El máximo es de 8 lecturas.

## Cómo funciona

1. Se leen la temperatura y la humedad y se valida que estén dentro del rango del sensor.
2. Se suma 1 al contador de lecturas y se actualizan los mínimos, máximos, sumas y secuencias.
3. Se clasifica la lectura:
   - **Crítico:** temperatura o humedad fuera del rango crítico. Se genera una alerta crítica y se termina.
   - **Óptimo:** las dos variables están en el rango óptimo. Si es la primera lectura queda "Condiciones óptimas" y si no, "Cultivo estabilizado". Se termina.
   - **Observación:** cualquier otro caso. Se aplican acciones correctivas (calefacción, ventilar, deshumidificar o nebulizar, y si fallan las dos variables se combinan). Si ya van 8 lecturas se hace una revisión técnica de los equipos y se termina.
4. Si no se terminó, se pide otra lectura.
5. Al final se calculan los promedios y se imprime el resultado.

### Resultados posibles

- **Alerta crítica:** hubo una lectura crítica.
- **Condiciones óptimas:** la primera lectura ya estaba en rango óptimo.
- **Cultivo estabilizado:** estaba en observación y luego llegó al rango óptimo.
- **Revisión técnica:** pasaron 8 lecturas sin llegar a lo óptimo.

## Archivos del repositorio

| Archivo | Qué es |
| --- | --- |
| `invernadero.py` | El código del programa en Python |
| `Explicacion_diagrama_de_flujo.docx` | Explicación paso a paso del diagrama de flujo |
| `Analisis_y_Prueba_de_Diseño_Parcial_2.xlsx` | Análisis (entradas, procesos y salidas) y pruebas de escritorio |
| `Tabla_identificadores_Invernadero.xlsx` | Tabla con todas las variables y constantes del programa |

## Cómo ejecutarlo

Se necesita tener Python 3 instalado. Desde la carpeta del repositorio:

```
python invernadero.py
```

El programa pide la temperatura y la humedad en cada lectura. Se puede escribir con coma o con punto (por ejemplo `25,5` o `25.5`).

## Pruebas

En el Excel de análisis hay 5 casos de prueba hechos a mano (prueba de escritorio):

| Caso | Qué pasa | Resultado |
| --- | --- | --- |
| 1 | Empieza en 29 °C y 75 %, se corrige y se estabiliza en la lectura 4 | Cultivo estabilizado |
| 2 | La humedad va bajando hasta 38 % en la lectura 4 | Alerta crítica |
| 3 | Pasan 8 lecturas sin llegar a lo óptimo | Revisión técnica |
| 4 | Primera lectura de 22 °C y 68 % | Condiciones óptimas |
| 5 | Se digita una humedad de 105 % por error y se vuelve a pedir | Condiciones óptimas |

### Ejemplo (caso 2)

Entradas: `22/55`, `21/50`, `23/46`, `24/38`

```
Lectura 1 | 22 °C | 55 % | Observación | Nebulizar
Lectura 2 | 21 °C | 50 % | Observación | Nebulizar
Lectura 3 | 23 °C | 46 % | Observación | Nebulizar
Lectura 4 | 24 °C | 38 % | Crítico | Alerta crítica: activar protocolo de emergencia

Resultado: Alerta crítica. Lecturas tomadas: 4.
Temperatura: mínima 21 – máxima 24 – promedio 22,50.
Humedad: mínima 38 – máxima 55 – promedio 47,25.
Secuencia de temperaturas: 22; 21; 23; 24. Secuencia de humedades: 55; 50; 46; 38.
```
