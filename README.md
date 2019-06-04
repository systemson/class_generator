# class_generator
Generate php Class files.

### Implementing Interface methods.

interface TestInterface
{
    public function testMethod(int $num, string $string): bool;
}

class ParentClass
{
    abstract public function abstractMethod(int $num, string $string): bool;
}

$maker = new Maker();

$output = $maker->getImplementingClass('ClassName', 'TestInterface');

echo $output;
/*
<?php

class ClassName implements TestInterface
{
    public function testMethod(int $num, string $string): bool
    {
        //
    }
}
*/

$output = $maker->getExtendingClass('ClassName', ''ParentClass', 'TestInterface');

echo output;

/*
<?php

class ClassName extends ParentClass implements TestInterface
{
    public function testMethod(int $num, string $string): bool
    {
        //
    }
    
    public function abstractMethod(int $num, string $string): bool
    {
        //
    }
}
*/

Adding full class namespace
$output = $maker->getExtendingClass('Full\Namespace\ClassName', ''ParentClass', 'TestInterface');
or
$output = $maker->getImplementingClass('Full\Namespace\ClassName', 'TestInterface');
/*
...
namespace Full\Namespace;

class ClassName ...

*/

Adding full namespaces for parent classes and implementing interfaces will put the full name in a use statement, and use the shot name instead.


$output = $maker->getExtendingClass('ClassName', 'Full\Namespace\ParentClass', 'Full\Namespace\TestInterface');

...
use Full\Namespace\ParentClass;
use Full\Namespace\TestInterface;

class ClasName extends ParentClass implements TestInterface
...

Finally if the type hint for parameters and return types is a class, the full namespace will be in a use statement, and the short name will be used too.

use Full\Namespace\TestInterface;

class ParentClass
{
    abstract public function test(TestInterface $test): TestInterface
}


$output = $maker->getExtendingClass('ClassName', 'ParentClass');

echo $output;
/*
use Full\Namespace\TestInterface;

class ClassName extends ParentClass
{
    public function test(TestInterface $test): TestInterface
    {
        //
    }
}
*/
