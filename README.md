## Requirements

* php-gedcom 1.0+ requires PHP 8.0 (or later).

## Installation

There are two ways of installing php-gedcom.

### Download and __autoload

If you are not using composer, you can download an archive of the source from GitHub and extract it into your project. You'll need to setup an autoloader for the files, unless you go through the painstaking process if requiring all the needed files one-by-one. Something like the following should suffice:

```php
spl_autoload_register(function ($class) {
    $pathToGedcom = __DIR__ . '/library/'; // TODO FIXME

    if (!substr(ltrim($class, '\\'), 0, 7) == 'Gedcom\\') {
        return;
    }

    $class = str_replace('\\', DIRECTORY_SEPARATOR, $class) . '.php';
    if (file_exists($pathToGedcom . $class)) {
        require_once($pathToGedcom . $class);
    }
});
```

### Usage

To parse a GEDCOM file and load it into a collection of PHP Objects, simply instantiate a new Parser object and pass it the file name to parse. The resulting Gedcom object will contain all the information stored within the supplied GEDCOM file:

```php
$parser = new \Gedcom\Parser();
$gedcom = $parser->parse('tmp.ged');

foreach ($gedcom->getIndi() as $individual) {
    echo $individual->getId() . ': ' . current($individual->getName())->getSurn() .
        ', ' . current($indi->$individual())->getGivn();
}
```
