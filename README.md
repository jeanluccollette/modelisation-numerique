# Modélisation numérique

## Introduction

On se propose de détailler sur un exemple les  étapes suivies pour accéder à la fonction de transfert $H_N(z)$ modélisant l'ensemble encadré en jaune dans le schéma ci-dessous.

![](csd_1a_pr.jpg)

Le convertisseur numérique analogique (CN/A) est un bloqueur d'ordre zéro (_zero order hold_), de sorte que $e(t)=e_N(n)$ pour $nT_e \leq t \lt (n+1)T_e$.

Le convertisseur analogique numérique (CA/N) délivre un signal numérique $s_N(n)=s(nT_e)$.
