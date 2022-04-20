---
layout: blog
title: Operadores ternarios en JavaScript
date: 2022-04-20T12:40:26.019Z
---
<!--StartFragment-->

En primer lugar, una expresión ternaria no es un reemplazo para una construcción if / else, es un equivalente a una construcción if / else que **devuelve** un valor. Es decir, una cláusula if / else es código, una expresión ternaria es una **expresión** , lo que significa que devuelve un valor.

Esto significa varias cosas:

* use expresiones ternarias solo cuando tenga una variable en el lado izquierdo del `=` que se le asignará el valor de retorno
* solo use expresiones ternarias cuando el valor devuelto sea uno de dos valores (o use expresiones anidadas si eso es apropiado)
* cada parte de la expresión (después de? y después:) debe devolver un valor sin efectos secundarios (la expresión `x = true`devuelve verdadero ya que todas las expresiones devuelven el último valor, pero también cambia x sin que x tenga ningún efecto en el valor devuelto)

En resumen: el uso 'correcto' de una expresión ternaria es

```javascript
var resultofexpression = conditionasboolean ? truepart: falsepart;
```

En lugar de su ejemplo `condition ? x=true : null ;`, donde usa una expresión ternaria para establecer el valor de `x`, puede usar esto:

```javascript
 condition && (x = true);
```

Esto sigue siendo una expresión y, por lo tanto, podría no pasar la validación, por lo que un enfoque aún mejor sería

```javascript
void(condition && x = true);
```

El último pasará la validación.

Pero, de nuevo, si el valor esperado es un valor booleano, simplemente use el resultado de la expresión de condición en sí

```javascript
var x = (condition); // var x = (foo == "bar");
```

- - -

**ACTUALIZACIÓN** En relación con su muestra, esto probablemente sea más apropiado:

```javascript
defaults.slideshowWidth = defaults.slideshowWidth || obj.find('img').width()+'px';
```

<!--EndFragment-->