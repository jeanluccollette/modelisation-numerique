# Modélisation numérique

## Introduction

On se propose de détailler sur un exemple les  étapes suivies pour accéder à la fonction de transfert $H_N(z)$ modélisant l'ensemble encadré en jaune dans le schéma ci-dessous.

![](csd_1a_pr.jpg)

Le convertisseur numérique analogique (CN/A) est un bloqueur d'ordre zéro (_zero order hold_), de sorte que $e(t)=e_N(n)$ pour $nT_e \leq t \lt (n+1)T_e$.

Le convertisseur analogique numérique (CA/N) délivre un signal numérique $s_N(n)=s(nT_e)$.

## Exemple choisi

Les étapes vont être détaillées avec la fonction de transfert ci-dessous.

$$H(p)=\\frac{K}{p \\left(p \\tau + 1\\right)}$$

## Réponse indicielle associée à $H(p)$

Via le package **sympy**, on accède à la réponse indicielle $r(t)$.

```python
import sympy as sp
p, zm1, K, tau, t, n, T_e=sp.symbols('p, z^{-1}, K, tau, t, n, T_e')
H = K/(p*(1+tau*p))
r = sp.inverse_laplace_transform(H/p,p,t)
```

$$r(t)=K \\left(t \\theta\\left(t\\right) - \\tau \\theta\\left(t\\right) + \\tau e^{- \\frac{t}{\\tau}} \\theta\\left(t\\right)\\right)$$

## Echantillonnage de la réponse indicielle

$$r_N(n) = K \\left(T_{e} n \\theta\\left(T_{e} n\\right) - \\tau \\theta\\left(T_{e} n\\right) + \\tau e^{- \\frac{T_{e} n}{\\tau}} \\theta\\left(T_{e} n\\right)\\right)$$

## Transformée en z de cette réponse

Pour cette étape, il faut faire appel à une table des transformées en z usuelles.

$$R_N(z)=\\frac{K T_{e} z^{-1}}{\\left(1 - z^{-1}\\right)^{2}} + \\frac{K \\tau}{- z^{-1} e^{- \\frac{T_{e}}{\\tau}} + 1} - \\frac{K \\tau}{1 - z^{-1}}$$

## Fonction de transfert $H_N(z)$

$$H_N(z) = (1-z^{-1})R_N(z)= \\left(1 - z^{-1}\\right) \\left(\\frac{K T_{e} z^{-1}}{\\left(1 - z^{-1}\\right)^{2}} + \\frac{K \\tau}{- z^{-1} e^{- \\frac{T_{e}}{\\tau}} + 1} - \\frac{K \\tau}{1 - z^{-1}}\\right)$$

## Expression finale de $H_N(z)$ sous forme de fraction rationnelle en $z^{-1}$

$$H_N(z) = - \\frac{K z^{-1} \\left(- T_{e} z^{-1} + T_{e} e^{\\frac{T_{e}}{\\tau}} + \\tau z^{-1} e^{\\frac{T_{e}}{\\tau}} - \\tau z^{-1} - \\tau e^{\\frac{T_{e}}{\\tau}} + \\tau\\right)}{\\left(- z^{-1} + e^{\\frac{T_{e}}{\\tau}}\\right) \\left(z^{-1} - 1\\right)}$$

## Conclusion

Les différentes étapes ont été illustrées avec une fonction de transfert $H(p)$ dont les coefficients sont exprimés sous forme littérale.

Dans des environnements tels que Matlab ou Python (avec le package **control**), il existe des méthodes (**c2d()**) réalisant directement ces étapes avec des fonctions de transfert $H(p)$ dont les coefficients sont exprimés sous forme numérique. Elles sont bien évidemment à privilégier dans un contexte classique d'asservissement où les paramètres des modèles sont déjà sous forme numérique via une identification du système. 

