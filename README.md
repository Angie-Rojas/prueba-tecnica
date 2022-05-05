# Prueba Técnica 1 :woman_technologist:
Aquí se encuantra la solución a los tres problemas de la parte 1 de la prueba técnica.

El desarrollo de estos problemas se realizó en Unity con el lenguaje C#, en este documento se encuentra el código de cada uno de estos ejercicios.

Ejecutable: https://ngie98.github.io/prueba-tecnica/

## Problema 1: Calcetines :socks:

Jhon trabaja en una tienda de ropa. Tiene una gran pila de calcetines que debe combinar por color para la venta. Dada una matriz de enteros que representan el color de cada calcetin, determina cuántos pares de calcetines con colores coincidentes hay.

Por ejemplo, hay n=7 calcetines con colores ar=[1,2,1,2,1,3,2]. Hay un par de colores 1 y uno de color 2. Quedan 3 calcetines extraños, uno de cada color. El número de pares es 2.

### Código Fuente:

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
    
    /*****      👉🏻 ENTRADA 👈🏻      *****/
    //En el método Strat se insertan los valores presentes en el problema, los cuales pueden ser modificados or el usuario
    void Start()
    {
        entry.text = "9, 10, 20, 20, 10, 10, 30, 50, 10, 20";
        globe.gameObject.SetActive(false);
    }
    //El método run se llama al presionar el botón "CALCULAR" 
    public void run()
    {
        /*****      👉🏻 PROCESO 👈🏻      *****/
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
                        /*****      👉🏻SALIDA 👈🏻      *****/
                        exit.text = "El número de pares es " + finish;
                        if (finish < 1)
                        {
                            /*****      👉🏻 SALIDA 👈🏻      *****/
                            exit.text = "No hay calcetines pares :(";
                        }
                    }
                }
            }
            //En esta función se verifica si el dato ya existe, si no existe, retorna true para dar permiso a la ejecución del condicional de la linea 62
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

## Problema 2: Números Enteros :1234:

Dados cinco enteros positivos, encuentre los valores mínimo y máximo que se pueden calcular sumando exactamente cuatrode los cinco enteros. Luego imprima los valores mínimos y máximos respectivos como una sola línea de dos enteros largos separados por espacios.

Por ejemplo arr = [1,3,5,7,9]. Nuestra suma mínima es 1+3+5+7=16 y nuestra suma máxima es 3+5+7+9=24

### Código Fuente:

``` c#

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;
using System.Linq;
using UnityEngine.SceneManagement;

public class Cumple : MonoBehaviour
{
    //Se llaman los elementos de la interfaz
    public TMP_Dropdown age;
    public TMP_InputField candle_1, candle_2, candle_3, candle_4, candle_5, candle_6, candle_7;
    public GameObject obj_4, obj_5, obj_6, obj_7;
    public TMP_Text exit;

    /*****      👉🏻 ENTRADA 👈🏻      *****/
    void Start()
    {
        age.value = 1;
        candle_1.text = "3";
        candle_2.text = "2";
        candle_3.text = "1";
        candle_4.text = "3";
    }

    // Aquí se activan o desactivan los espacios según la edad
    void Update()
    {
        switch (age.value)
        {
            case 0:
                obj_4.SetActive(false);
                obj_5.SetActive(false);
                obj_6.SetActive(false);
                obj_7.SetActive(false);
                candle_4.text = "0";
                candle_5.text = "0";
                candle_6.text = "0";
                candle_7.text = "0";
                break;
            case 1:
                obj_4.SetActive(true);
                obj_5.SetActive(false);
                obj_6.SetActive(false);
                obj_7.SetActive(false);
                candle_5.text = "0";
                candle_6.text = "0";
                candle_7.text = "0";
                break;
            case 2:
                obj_4.SetActive(true);
                obj_5.SetActive(true);
                obj_6.SetActive(false);
                obj_7.SetActive(false);
                candle_6.text = "0";
                candle_7.text = "0";
                break;
            case 3:
                obj_4.SetActive(true);
                obj_5.SetActive(true);
                obj_6.SetActive(true);
                obj_7.SetActive(false);
                candle_7.text = "0";
                break;
            case 4:
                obj_4.SetActive(true);
                obj_5.SetActive(true);
                obj_6.SetActive(true);
                obj_7.SetActive(true);
                break;
        }
    }

    // Este método se asigna al botón "CALCULAR"
    public void Operate()
    {

        /*****      👉🏻 PROCESO 👈🏻      *****/

        //Se asignan los valores a un Array String
        string[] arr =  { candle_1.text, candle_2.text, candle_3.text, candle_4.text, candle_5.text, candle_6.text, candle_7.text, };
        
        //Se pasa de Array String a Int String 
        int[] array = System.Array.ConvertAll(arr, int.Parse);
        
        //Se ordena el Array de forma desendente, tomando la primera posición para ser comparada
        int[] arrOrder = array.OrderByDescending(c => c).ToArray();
        int higher = arrOrder[0];
        int count = 0;

        //Se recorre el arreglo
        for (int i = 0; i < arrOrder.Length; i++)
        {
            //Se compara cada número con el número mayor, si coincide se aumenta el contador
            if (higher == arrOrder[i])
            {
                count++;
            }
        }

        /*****      👉🏻SALIDA 👈🏻      *****/
        exit.text = "Tu sobrina podrá soplar: " + count + " velas";
    }

    //Este método permite el cambio de vistas
    public void Prev()
    {
        SceneManager.LoadScene("Enteros");
    }
}



```


## Problema 3: Cumpleaños :birthday:

Estas a cargo del pastel para el cumpleaños de tu sobrina y has decidido que el pastel tendrá una vela por cada año de su edad total. Cuando ella apague las velas, solo podrá apaga las más altas. Tu tarea es averiguar cuántas velas puede apagar con éxito.
Por ejemplo, si tu sobrina está cumpliendo 4 años, y la tarta tendrá 4 velas de altura 4,4,1,3, ella sará capaz de soplar 2 velas con éxito, ya que las velas más altas son de altura 4 y aquí están 2 velas cn tal altura.

### Código Fuente:

``` c#


using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;
using System;
using System.Linq;
using UnityEngine.SceneManagement;

public class Enteros : MonoBehaviour
{
    public TMP_InputField input_0, input_1, input_2, input_3, input_4;
    public TMP_Text exit;

    /*****      👉🏻 ENTRADA 👈🏻      *****/
    void Start()
    {
        input_0.text = "1";   
        input_1.text = "2";   
        input_2.text = "3";   
        input_3.text = "4";   
        input_4.text = "5";
    }

    // Este método es llamado al presionar el botón "CALCULAR"
    public void Run()
    {
        /*****      👉🏻 PROCESO 👈🏻      *****/

        //Se convierten los strings ingresados por el usuario a int
        int arr_0 = Int32.Parse(input_0.text);
        int arr_1 = Int32.Parse(input_1.text);
        int arr_2 = Int32.Parse(input_2.text);
        int arr_3 = Int32.Parse(input_3.text);
        int arr_4 = Int32.Parse(input_4.text);

        //Se crea un arreglo al cual se le asignan los datos ingresados por el usuario
        int[] arr = new int[5];
        arr[0] = arr_0;
        arr[1] = arr_1;
        arr[2] = arr_2;
        arr[3] = arr_3;
        arr[4] = arr_4;

        //Se ordena el Array de manera descendente
        int[] arrOrder = arr.OrderByDescending(c => c).ToArray();
        //Se suman las posiciones cuatro primeras y cuatro últimas posiciones respectivamente
        int sumDes = arrOrder[0] + arrOrder[1] + arrOrder[2] + arrOrder[3];
        int sumAsc = arrOrder[1] + arrOrder[2] + arrOrder[3] + arrOrder[4];

        /*****      👉🏻 SALIDA 👈🏻      *****/
        exit.text = sumAsc + "  " + sumDes;
    }

    //Estos métodos permiten el cambio de vistas
    public void Prev()
    {
        SceneManager.LoadScene("Calcetines");
    }
    public void Next()
    {
        SceneManager.LoadScene("Cumple");
    }
}




```


