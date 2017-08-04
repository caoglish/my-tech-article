## PHP array_reduce()

```array_reduce``` reduces array into a single value. Basically, The ```array_reduce``` will go through every item with the result from last iteration and produce new value to the next iteration.

Usage:

```php

 array_reduce ($array, function($carry, $item){...}, $defaul_value_of_first_carry)

```

- $carry is the result from the last round of iteration.
- $item is the value of current position in the array.

### Sum of array

```php

    $result = array_reduce([1, 2, 3, 4, 5], function($carry, $item){
        return $carry + $item;
    });

```

result:```15```

### The largest number in array

```php

    $result = array_reduce([10, 23, 211, 34, 25], function($carry, $item){
            return $item > $carry ? $item : $carry;
    });

```

result:```211```


### Is all item more than 100

```php

    $result = array_reduce([101, 230, 210, 341, 251], function($carry, $item){
            return $carry && $item > 100;
    }, true); //default value must set true

```

result:```true```

### Is any item less than 100

```php

    $result = array_reduce([101, 230, 21, 341, 251], function($carry, $item){
            return $carry || $item < 100;
    }, false);//default value must set false

```

result:```true```

### Like implode($array, $piece)

```php

    $result = array_reduce(["hello", "world", "PHP", "language"], function($carry, $item){
            return !$carry ? $item : $carry . "-" . $item ;
    });

```

result:```"hello-world-PHP-language"```

if make a implode method, the source code will be :

```php

    function implode_method($array, $piece){
        return array_reduce($array, function($carry, $item) use ($piece) {
                return !$carry ? $item : ($carry . $piece . $item);
        });
    }

```

    $result = implode_method(["hello", "world", "PHP", "language"], "-");

result:```"hello-world-PHP-language"```
