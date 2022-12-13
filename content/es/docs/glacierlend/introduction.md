---
title: "Introducción"
description: "Un protocolo de liquidez con reglas claras"
# lead: "Un protocolo de liquidez con reglas claras"
date: 2022-12-07T00:00:00+00:00
lastmod: 2022-12-07T00:00:00+00:00
draft: false
images: []
menu:
  docs:
    parent: "glacierlend"
weight: 100
toc: true
---

Un protocolo de liquidez consiste en una plataforma en donde los usuarios depositan fondos (entregan liquidez) ya sea en criptoactivos o moneda fiat y, en caso de que estos sean prestados a otros usuarios, reciben una recompensa en forma de interés. El protocolo permite a sus usuarios pedir préstamos de esos fondos, al considerar sus depósitos como garantía. En GlacierLend, nuestro sistema de intereses incentiva el pago de préstamos por parte de borrowers y el depósito de capital por parte de lenders, fomentando la participación de ambas partes.

GlacierLend, nuestro fondo de liquidez, funciona en base a lenders, quienes son usuarios que depositan su dinero –hasta ahora, solamente en forma de pesos chilenos– en nuestro protocolo. Por el otro lado, están los borrowers, que dejan criptoactivos en garantía –de momento solo permitimos ETH– para poder acceder al dinero depositado.

## Incentivo a través de intereses

Nuestro modelo de intereses es definido por el rol que cada usuario juega dentro de nuestro fondo. Basándonos en la oferta y demanda, los intereses van aumentando o decreciendo, ya sea por una mayor utilización del fondo por parte de los borrowers (demanda) o bien por un mayor ingreso de capital por parte de los lenders (oferta).

![intereses](https://miro.medium.com/max/4800/1*r4SqSE6NFuzCWGiEd2pJig.webp)

De esta forma, nuestro sistema de intereses incentiva el pago de préstamos por parte de borrowers y el depósito de capital por parte de lenders, fomentando la participación de ambas partes en nuestro fondo.

Los borrowers pueden pedir préstamos en la medida que el valor del criptoactivo dejado en garantía sea mayor al préstamo solicitado, el cual puede llegar como máximo al 70 % del valor que tenga la garantía en el momento en que se solicita el préstamo. Además, estos usuarios tendrán un plazo de 365 días para devolver la deuda contraída, sumando los intereses acumulados de forma diaria.

En un escenario de no pago o si la garantía pierda valor, parte de su criptoactivo depositado será liquidado para pagar la deuda contraída. El valor de la garantía es monitoreado de forma constante, de acuerdo a los precios que nos provee [Chainlink](https://0xglacier.medium.com/glacier-integrates-chainlink-price-feeds-to-facilitate-cedefi-lending-and-borrowing-592c73f4fc3c).

## Liquidación y distribución de recursos

En GlacierLend utilizamos un concepto llamado liquidación pasiva. Este funciona de la siguiente forma: un borrower deja ETH como colateral por su préstamo. Si el 75 % del precio del colateral es menor a la deuda contraída, el 50 % de este criptoactivo es transformado a una stablecoin (en nuestro caso, USDC). Estos quedarán disponibles para que cualquier usuario los pueda comprar a precio fijo y sin comisiones.

Sin embargo, para prevenir una posible liquidación, la plataforma le notifica en cada momento al borrower el estado del colateral dejado en garantía, para que pueda tomar las acciones necesarias, como pagar parte de su deuda o depositar más colateral.

En el caso de que un borrower haya sufrido un evento de liquidación pasiva y, luego realice el pago total de su deuda, entonces podrá recuperar el resto de su colateral y el USDC que aún no haya sido comprado por otro usuario.

Vale la pena recalcar que en el caso de una liquidación pasiva, el usuario deberá pagar una multa, correspondiente al 10 % de la liquidación. Buscamos que la multa recaudada sea distribuida dentro del mismo ecosistema, asegurando así una base financiera sana para quienes utilicen GlacierLend. Aquella multa se destinará de la siguiente manera:

![Liquidación](https://miro.medium.com/max/1400/1*BkX1mSdtVWkn2evmRQz32Q.webp)

Cuando los lenders desean dejar de participar del protocolo, deberán informar con cinco días de anticipación y, en caso de que en el quinto día no se cuente con la liquidez necesaria, GlacierLend puede también liquidar –en caso de que los hubiese– los USDC obtenidos por la liquidación pasiva y utilizar este capital para intentar cubrir los fondos solicitados.

Sin embargo, el protocolo no garantiza liquidez, sino que se respalda en el modelo de intereses para incentivar esta liquidez. En períodos de extrema demanda, la liquidez del fondo (es decir, los fondos disponibles para retirar o prestar) disminuirá, aumentando las tasas de interés, incentivando así la oferta y desincentivando la demanda.
