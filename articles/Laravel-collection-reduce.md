## Laravel Collection Reduce

<!-- Language-All: php -->
The ```reduce``` method reduces the collection to a single value, passing the result of each iteration into the subsequent iteration. Please see [reduce method][1].

The ```reduce``` method loops through each item with a collection and produces new result to the next iteration. Each result from the last iteration is passed through the first parameter (in the following examples, as ```$carry```).

This method can do a lot of processing on large data sets. For example the following examples, we will use the following example student data:

```php
     $student = [
        ['class' => 'Math', 'score' => 60],
        ['class' => 'English', 'score' => 61],
        ['class' => 'Chemistry', 'score' => 50],
        ['class' => 'Physics', 'score' => 49],
    ];
```

### Sum student's total score

```php
    $sum = collect($student)
        ->reduce(function($carry, $item){
            return $carry + $item["score"];
        }, 0);
```

Result: ```220```

Explanation:

- ```$carry``` is the result from the last iteration. 
- The second parameter is the default value for the $carry in the first round of iteration. This case, the default value is 0

### Pass a student if all their scores are >= 50

```php
    $isPass = collect($student)
        ->reduce(function($carry, $item){
            return $carry && $item["score"] >= 50;
        }, true);
```

Result: ```false```

Explanation:

- Default value of $carry is true
- If all score is greater than 50, the result will return true; if any less than 50, return false.

### Fail a student if any score is < 50

```php
    $isFail = collect($student)
        ->reduce(function($carry, $item){
            return $carry || $item["score"] < 50;
        }, false);
```

Result: ```true```

Explain:

- the default value of $carry is false
- if any score is less than 50, return true; if all scores are greater than 50, return false.

### Return subject with the highest score

```php
    $highestSubject = collect($student)
        ->reduce(function($carry, $item){
            return $carry === null || $item["score"] > $carry["score"] ? $item : $carry;
        });
```

result: ```[ "subject" => "English", "score" => 61 ]```

Explain:

- The second parameter is not provided in this case.
- The default value of $carry is null, thus we check for that in our conditional.

  [1]: https://laravel.com/docs/5.2/collections#method-reduce