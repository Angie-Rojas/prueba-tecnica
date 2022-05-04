# Prueba Técnica 1
Aquí se encuantra la solución a los tres problemas de la parte 1 de la prueba técnica.

El desarrollo de estos problemas se realizó en Unity con el lenguaje C#, en este documento se encuentra el código de cada uno de estos ejercicios

## Problema 1: Calcetines

Jhon trabaja en una tienda de ropa. Tiene una gran pila de calcetines que debe combinar por color para la venta. Dada una matriz de enteros que representan el color de cada calcetin, determina cuántos pares de calcetines con colores coincidentes hay.

Por ejemplo, hay n=7 calcetines con colores ar=[1,2,1,2,1,3,2]. Hay un par de colores 1 y uno de color 2. Quedan 3 calcetines extraños, uno de cada color. El número de pares es 2.

```C#

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
using System.Text.RegularExpressions;
using UnityEngine.SceneManagement;

public class Calcetines : MonoBehaviour
{
    //Aquí se llaman los elementos de la interfaz
    public TMP_InputField entry;
    public TMP_Text exit;
    public GameObject globe;
    //En el método Strat se insertan los valores presentes en el problema, los cuales pueden ser modificados or el usuario
    void Start()
    {
        entry.text = "9, 10, 20, 20, 10, 10, 30, 50, 10, 20";
        globe.gameObject.SetActive(false);
    }
    //El método run se llama al presionar el botón "CALCULAR" 
    public void run()
    {
        //Esta cadena corresponde a la ingresada por el usuario en la interfaz
        string strOne = entry.text;
        //Aquí se asignan Regex a diferentes variables para que el programa pueda determinar cuando el usuario ingresa valores diferentes a números y a comas.
        var upper = new Regex(@"[A-Z]+");
        var lower = new Regex(@"[a-z]+");
        var symbols = new Regex(@"[!@#$%^&*()_+=\[{\]};:<>|./?-]");
        //Este condicional determina si el usuario ingreso algún carácter presente en los Regex
        //Si se ingresa al condicional se muestra una alerta para que el usuario pueda recuperarse de su error (Heurística de Nielsen).
        if (upper.IsMatch(strOne) || lower.IsMatch(strOne) || symbols.IsMatch(strOne) || strOne == "")
        {
            globe.gameObject.SetActive(true);
        }
        //Si no entra a ninguno de los condicionales anteriores, el programa inicia las operaciones con los valores ingresados o por defecto
        else
        {
            //Se asigna el String a un String Array, se separa cada valor por la coma ingresada por el usuario
            string[] strArrayOne = new string[] { "" };
            strArrayOne = strOne.Split(',');


            int finish = 0;
            int result = 0;
            //String Array pasa a ser Int Array
            int[] array = System.Array.ConvertAll(strArrayOne, int.Parse);
            int[] arrayTwo = new int[array.Length];
            //Se inicia un ciclo que recorre las posiciones del Array 
            for (int i = 0; i < array.Length; i++)
            {
                int count = 0;
                //Se inicia otro ciclo que compara los valores entre cada una de las posiciones
                for (int j = 0; j < array.Length; j++)
                {
                    if (array[i] == array[j])
                    {
                        count++;
                        //Aquí se llena el Array arrayTwo con los datos sin repetir del Array principal
                        if (numero(array[i]))
                        {
                            arrayTwo[i] = array[i];
                        }
                    }
                }
                //Se verifica la cantidad de veces que estan los datos, ignorando los espacios vacios
                if (arrayTwo[i] != 0)
                {
                    if (count >= 2)
                    {
                        result = count / 2;
                        //Se suma la cantidad de pares
                        finish = finish + result;
                        exit.text = "El número de pares es " + finish;
                        if (finish < 1)
                        {
                            exit.text = "No hay calcetines pares :(";
                        }
                    }
                }
            }
            //En esta función se verifica si el dato ya existe, si no existe, retorna true para dar permiso a la ejecución del condicional de la linea 60
            bool numero(int num)
            {
                for (int i = 0; i < arrayTwo.Length; i++)
                {
                    if (arrayTwo[i] == num)
                    {
                        return false;
                    }
                }
                return true;
            }
        }
    }
    //Este método cierra la ventana de alerta
    public void close()
    {
        globe.gameObject.SetActive(false);
    }

    //Este método permite el cambio de vistas
    public void Next()
    {
        SceneManager.LoadScene("Enteros");
    }
}

```

