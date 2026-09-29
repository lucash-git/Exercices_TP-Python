Fichier de réponse à l'exercice 3

Réponse question 1 : 

import pandas as pd



df = pd.read\_csv('./data/Table.csv', sep='\\t')

df





Réponse question 2 : 



print(df.iloc\[:,3])



rho\_g\_per\_cm3 = 1.03

df\['Masse \[g]'] = rho\_g\_per\_cm3 \* df.iloc\[:,3]

df


Réponse question 3 : 

m\_foie\_lobe\_d = df.loc\[2,'Masse \[g]']

print(f'Masse du lobe {m\_foie\_lobe\_d:.2f} g')

Masse du lobe 833.85 g



delta\_Mev\_per\_Bq\_s = 0.9336

T\_y90\_s = 64.05\*3600

dose\_foie\_limite\_Gy = 120

act\_1 = (m\_foie\_lobe\_d\*1e-3 \*dose\_foie\_limite\_Gy\*np.log(2))/(delta\_Mev\_per\_Bq\_s\*1e6\*1.6e-19 \* T\_y90\_s)

print(f"L'activité à injecter est de {act\_1\*1e-9:.2f} GBq pour atteindre {dose\_foie\_limite\_Gy} Gy au lobe droit.")
L'activité à injecter est de 2.01 GBq pour atteindre 120 Gy au lobe droit.



Réponse question 4 :



act\_tum = df.iloc\[3,6]

act\_foie\_sain = df.iloc\[2,6]

print(act\_tum)

print(act\_foie\_sain)

ratio\_tum\_lobe = act\_tum/ act\_foie\_sain 

print(f"Le rapport des concentrations est estimé à {ratio\_tum\_lobe:.3f}")

5341.22

,1526.33

,Le rapport des concentrations est estimé à 3.499



m\_tum = df.iloc\[3,9]

print((m\_tum))

A\_n = act\_1 / (1+ratio\_tum\_lobe\*(m\_tum/m\_foie\_lobe\_d))

A\_t = ratio\_tum\_lobe \* A\_n\*(m\_tum)/(m\_foie\_lobe\_d)

print(f'Les activités dans le foie perfusé et la tumeur sont {A\_n\*1e-6:.2f} et {A\_t\*1e-6:.2f} MBq respectivement.')

10.1395981

,Les activités dans le foie perfusé et la tumeur sont 1931.50 et 82.19 MBq respectivement.



act\_cum = A\_t\*T\_y90\_s /np.log(2) 

dose\_t = act\_cum\*delta\_Mev\_per\_Bq\_s\*1e6\*1.6e-19 / (m\_tum\*1e-3)

print(f'La dose à la tumeur est {dose\_t:.2f} Gy')



La dose à la tumeur est 402.79 Gy

