# Втора задача

Напишете следите четири функции:

## groupby

Да се напише функция `groupby(func, seq)`, връщаща речник. Вторият аргумент е итеруем обект. Първият е функция, която връща ключовете от резултатния речник.
За стойности се взимат списъци, съдържащи обектите от `seq`, без да се нарушава редът им, групирани по съответния ключ.

    >>> groupby(lambda x: x % 2, [0,1,2,3,4,5,6,7])
    {0: [0, 2, 4, 6], 1: [1, 3, 5, 7]}

## iterate

Да се напише функция-генератор `iterate(func)`, която последователно връща функциите:<br />
identity, func, func.func,  func.func.func... и т.н.<br />
... където `identity` е функцията идентитет, а `.` е оператор за композиране на функции


    >>> def double(x):
            return 2 * x

    >>> i = iterate(double)
    >>> f = next(i)
    >>> f(3)
    3
    >>> f = next(i)
    >>> f(3)
    6
    >>> f = next(i)
    >>> f(3)
    12
    >>> f = next(i)
    >>> f(3)
    24
    >>> # и т.н.

## zip_with

Да се напише функция-генератор `zip_with(func, *iterables)`, която приема функция `func` и променлив брой итеруеми - `iterables`.
За всяко число `i` от 0 до дължината на най-късото итеруемо, прилага към функцията `func` аргументите взети от `i`-тата позиция. След това yield-ва резултата.
Ако не бъдат подадени `iterables` - генераторът трябва да бъде празен (да има 0 елемента).

    >>> def concat3(x, y, z):
    	    return x + y + z

    >>> first_names = ['John', 'Miles']
    >>> last_names = ['Coltrane', 'Davis']
    >>> spaces = [' '] * 2
    >>> list(zip_with(concat3, first_names, spaces, last_names))
    ['John Coltrane', 'Miles Davis']

## cache

Да се напише функция `cache(func, cache_size)`, която приема функция `func` и връща нова функция (ще я наричаме `func_cached`).
`func_cached` пази кеширани последните `cache_size` на брой уникални извиквания. Под "кеширани" разбираме, че при първото извикване с дадени аргументи, резултатът ще се изчисли от функцията `func`. При следващите извиквания, ще се връща вече изчисленият резултат.

Забележки:

* Не се очаква функцията `cache` да работи за именовани параметри, а единствено за позиционни.
* Не се очаква да работи за mutable аргументи, а единствено за immutable.
* За еднакви аргументи считайте такива, които при сравняване с `==` връщат `True`

Пример:

    >>> def double(x):
            print('called "double"')
            return x * 2

    >>> double_cached = cache(double, 2)
    >>> double_cached(1)
    called "double"
    2
    >>> double_cached(1)
    2
    >>> double_cached(2)
    called "double"
    4
    >>> double_cached(3)
    called "double"
    6
    >>> double_cached(3)
    6
    >>> double_cached(1) # извикванията с `2` и `3` са го измиестили от кеша
    called "double"
    2
