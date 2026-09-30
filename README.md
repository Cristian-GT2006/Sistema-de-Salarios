# Sistema-de-Salarios
# 💰 Sistema de Gestión y Análisis de Salarios

Este repositorio contiene una solución interactiva basada en consola diseñada para administrar, analizar y procesar datos financieros relacionados con salarios de empleados. Permite la captura dinámica de información, cálculo de métricas estadísticas en tiempo real y persistencia lógica durante la sesión de ejecución.

**Autor:** Cristian Gómez T.  
**Materia:** Programación / Estructuras de Control  

---

## 📋 1. Definición del Problema

El objetivo es diseñar un sistema interactivo que opere de forma continua a través de un menú dinámico. El software procesa entradas numéricas hasta recibir una señal de parada (número negativo), calcula métricas estadísticas esenciales (totales, promedios, máximos y mínimos) y garantiza la estabilidad del sistema mediante el control de excepciones lógicas (prevención estricta de división por cero cuando no existen datos).

---

## 📊 2. Análisis de Entradas, Procesos y Salidas

| Componente | Descripción |
| :--- | :--- |
| **Entradas** | <ul><li>`opcion`: Selección del menú principal (Entero).</li><li>`salario_ingresado`: Calificación o dato financiero dinámico (Real).</li><li>`salario_buscar`: Valor específico para comparación (Real).</li></ul> |
| **Procesos** | <ul><li>**Control:** Menú repetitivo condicionado con validación de opciones.</li><li>**Acumulación:** Adición iterativa de salarios válidos ingresados.</li><li>**Conteo:** Registro incremental de la cantidad de registros procesados.</li><li>**Cálculo Estadístico:** Determinación de la media aritmética (`Acumulador / Contador`).</li><li>**Búsqueda de Extremos:** Filtro lógico secuencial para hallar el salario máximo y mínimo.</li><li>**Validación:** Bloqueo de operaciones aritméticas críticas si el contador es igual a cero.</li><li>**Reinicio:** Restablecimiento completo de variables a su estado de inicialización.</li></ul> |
| **Salidas** | <ul><li>**Resumen en pantalla:** Total de empleados, monto acumulado, promedio de ingresos, salario máximo y salario mínimo.</li><li>**Resultado de comparación:** Mensaje de relación (Mayor, menor o igual al promedio).</li><li>Notificaciones de éxito, alertas del sistema o mensajes de error de entrada.</li></ul> |

---

## 💻 3. Pseudocódigo (Lógica Base)

```text
Algoritmo Sistema_Salarios
    // Definición de variables globales al menú
    Definir opcion Como Entero
    Definir contador Como Entero
    Definir acumulador, salario_mayor, salario_menor Como Real
    Definir salario_ingresado, salario_buscar, promedio Como Real
     
    // Inicialización de variables (Estado inicial)
    contador <- 0
    acumulador <- 0.0
    salario_mayor <- 0.0
    salario_menor <- 0.0
     
    Repetir
        Escribir ""
        Escribir "===== SISTEMA DE SALARIOS ====="
        Escribir "1. Registrar salarios"
        Escribir "2. Mostrar resumen"
        Escribir "3. Comparar un salario con el promedio"
        Escribir "4. Reiniciar informacion"
        Escribir "0. Salir"
        Escribir "Seleccione una opcion: "
        Leer opcion
         
        Segun opcion Hacer
            1:
                Escribir ""
                Escribir "--- Registro de Salarios ---"
                Escribir "Ingrese los salarios (ingrese un numero negativo para terminar):"
                Escribir "-> "
                Leer salario_ingresado
                 
                Mientras salario_ingresado >= 0 Hacer
                    Si contador = 0 Entonces
                        salario_mayor <- salario_ingresado
                        salario_menor <- salario_ingresado
                    Sino
                        Si salario_ingresado > salario_mayor Entonces
                            salario_mayor <- salario_ingresado
                        FinSi
                        Si salario_ingresado < salario_menor Entonces
                            salario_menor <- salario_ingresado
                        FinSi
                    FinSi
                     
                    acumulador <- acumulador + salario_ingresado
                    contador <- contador + 1
                     
                    Escribir "-> "
                    Leer salario_ingresado
                FinMientras
                Escribir "Registro finalizado. Se registraron ", contador, " salarios."
                 
            2:
                Escribir ""
                Escribir "--- Resumen de Salarios ---"
                Si contador = 0 Entonces
                    Escribir "No hay salarios registrados en el sistema."
                Sino
                    promedio <- acumulador / contador
                    Escribir "Total de salarios registrados: ", contador
                    Escribir "Monto total acumulado: $", acumulador
                    Escribir "Salario promedio: $", promedio
                    Escribir "Salario mayor: $", salario_mayor
                    Escribir "Salario menor: $", salario_menor
                FinSi
                 
            3:
                Escribir ""
                Escribir "--- Comparar Salario ---"
                Si contador = 0 Entonces
                    Escribir "No se puede comparar. Primero debe registrar salarios."
                Sino
                    promedio <- acumulador / contador
                    Escribir "Ingrese el salario que desea comparar: $"
                    Leer salario_buscar
                     
                    Si salario_buscar > promedio Entonces
                        Escribir "El salario de $", salario_buscar, " esta POR ENCIMA del promedio ($", promedio, ")."
                    Sino
                        Si salario_buscar < promedio Entonces
                            Escribir "El salario de $", salario_buscar, " esta POR DEBAJO del promedio ($", promedio, ")."
                        Sino
                            Escribir "El salario de $", salario_buscar, " es IGUAL al promedio ($", promedio, ")."
                        FinSi
                    FinSi
                FinSi
                 
            4:
                contador <- 0
                acumulador <- 0.0
                salario_mayor <- 0.0
                salario_menor <- 0.0
                Escribir ""
                Escribir "[!] Toda la informacion ha sido reiniciada con exito."
                 
            0:
                Escribir ""
                Escribir "Saliendo del sistema. ¡Hasta luego!"
                 
            De Otro Modo:
                Escribir ""
                Escribir "[Error] Opcion invalida. Intente de nuevo."
        FinSegun
         
    Hasta Que opcion = 0
FinAlgoritmo
```

---

## ☕ 4. Código Fuente (Java)

La implementación en **Java** utiliza estructuras limpias, control de flujo optimizado y formato de salida numérico de alta precisión para valores monetarios.

```java
import java.util.Scanner;

public class SistemaSalarios {
    public static void main(String[] args) {
        Scanner teclado = new Scanner(System.in);
        
        // Declaración e inicialización de variables de estado
        int opcion;
        int contador = 0;
        double acumulador = 0.0;
        double salarioMayor = 0.0;
        double salarioMenor = 0.0;
        
        double salarioIngresado;
        double salarioBuscar;
        double promedio;

        // Bucle principal del menú iterativo
        do {
            System.out.println("\n===== SISTEMA DE SALARIOS =====");
            System.out.println("1. Registrar salarios");
            System.out.println("2. Mostrar resumen");
            System.out.println("3. Comparar un salario con el promedio");
            System.out.println("4. Reiniciar informacion");
            System.out.println("0. Salir");
            System.out.print("Seleccione una opcion: ");
            opcion = teclado.nextInt();

            switch (opcion) {
                case 1:
                    System.out.println("\n--- Registro de Salarios ---");
                    System.out.println("Ingrese los salarios (ingrese un numero negativo para terminar):");
                    System.out.print("-> ");
                    salarioIngresado = teclado.nextDouble();

                    // Registro iterativo controlado por bandera negativa
                    while (salarioIngresado >= 0) {
                        if (contador == 0) {
                            salarioMayor = salarioIngresado;
                            salarioMenor = salarioIngresado;
                        } else {
                            if (salarioIngresado > salarioMayor) {
                                salarioMayor = salarioIngresado;
                            }
                            if (salarioIngresado < salarioMenor) {
                                salarioMenor = salarioIngresado;
                            }
                        }

                        acumulador += salarioIngresado;
                        contador++;

                        System.out.print("-> ");
                        salarioIngresado = teclado.nextDouble();
                    }
                    System.out.println("Registro finalizado. " + contador + " salarios almacenados.");
                    break;

                case 2:
                    System.out.println("\n--- Resumen de Salarios ---");
                    // Protección anti división por cero
                    if (contador == 0) {
                        System.out.println("[!] No hay salarios registrados en el sistema.");
                    } else {
                        promedio = acumulador / contador;
                        System.out.println("Total de salarios registrados: " + contador);
                        System.out.printf("Monto total acumulado: $%.2f\n", acumulador);
                        System.out.printf("Salario promedio: $%.2f\n", promedio);
