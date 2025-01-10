# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Полушин Максим Викторович
- РИ231122
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Реализовать перцептрон в проекте Unity

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления:
OR | дать комментарии о корректности работы

AND | дать комментарии о корректности работы

NAND | дать комментарии о корректности работы

XOR | дать комментарии о корректности работы

Ход работы:
- Создать пустой проект на Unity
- Добавить пустой объект и подключить к нему cs файл со следующим кодом:
```py
﻿using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```

1)OR. Работает корректно, необходимо 3 эпохи, чтобы перцептрон работал без ошибок.
![image](https://github.com/user-attachments/assets/1134225f-b9fa-440b-9437-cac553a5ebbf)

2)AND. Работает корректно, необходимо 3 эпохи, чтобы перцептрон работал без ошибок.
![image](https://github.com/user-attachments/assets/c972cf84-7730-4ced-86fd-a90df0ea0c1e)

3)NAND. Работает корректно, необходимо 3 эпохи, чтобы перцептрон работал без ошибок.
![image](https://github.com/user-attachments/assets/a0d8cf6a-38b2-4e77-a9ed-60ccc6442bca)

4)XOR. Работает некорректно, т.к перцептрон работает только с линейными функциями, а XOR - нелинейная.
![image](https://github.com/user-attachments/assets/647357a1-03ae-46df-be85-7517aca0ae84)











## Задание 2
### Построить графики зависимости количества эпох от ошибки  обучения. Указать от чего зависит необходимое количество эпох обучения.

- Ход работы: Заполнить google-таблицу данными об эпохах и визуализировать их с помощью графиков.
1.OR

![image](https://github.com/user-attachments/assets/bef54113-6303-4ff7-ab5e-be9d3baaada7)

2.AND

![image](https://github.com/user-attachments/assets/e9f2bd02-581c-40d6-8244-7439627160a4)

3.NAND

![image](https://github.com/user-attachments/assets/7509a783-c034-4504-ba98-ad47c1a0ee26)

4.XOR

![image](https://github.com/user-attachments/assets/73a994df-4710-4164-a901-268bf43d483a)





## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.


## Выводы

В ходе выполнения данной работы я узнал что такое персептрон, познакомился с его работой, а также с задачами, которые он может выполнять.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
