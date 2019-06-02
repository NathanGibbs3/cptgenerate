# cptgenerate -- JIT PHPUnit Test Generation
Build Unit tests for diverse PHPUnit versions from a master set of PHPUnit
tests.

Generates a single set of Unit tests based on supplied PHPUnit version or
multiple test sets that can be run by PHPUnit based on installed PHP version.

## This project enables developers to:
1. Build with all default PHP Major.Minor versions available on travis-ci.
1. Build with default PHP/PHPUnit combinations avaliable on travis-ci.
1. Maintain one set of Unit tests.
1. Spend less time maintaining Unit tests.
1. Spend more time writing code. :smile:

# History:
While working on [BASE](https://github.com/NathanGibbs3/BASE), we ended up
with test sets for 3 different versions of PHPUnit. Occasionally, builds
failed or did not have uniform code coverage as maintaining the Unit test sets
was a manual process. Local testing in VM's also raised issues with
PHP/PHPUnit combinations not seen via CI. Additionally, ~90% of the code
in each Unit test set was identical.

## The differnences between each test set were:
1. Class defines.
  1. Namespaced.
  1. Non-Namespaced.
1. Test fixture defines.
  1. Typehinted.
  1. Non-Typehinted.

## The solution:
`cptgenerate` which builds, from a master set of PHPUnit tests, a set of tests
compatible with the PHPUnit version used in the test environment.  
Basically, **JIT PHPUnit Test generation.**

# Usage:
Command Line Options are space sepearated. All locations are relative to
execution dir.

## Options:
1. Location of Master Test Set ( defaults to tests/php );
1. Location of Test Build ( defaults to tests/PhpUnit );
	If option is set to "multi" will search for multiple Test Set locations
	formated as tests/phpX.X
	Dir tests/php5.2 = Tests built as Non-Ns Non-Th
	Dir tests/php7.1 = Tests built as Ns Th
	Anything else defaults to Ns Non-Th
1. PHPUnit Version ( defaults to 0.0.0 )

# Usage Examples:
Command|Master Tests|Generated Tests
---|---|---
`php -f ./tests/phptestgen.php` | Located in ./tests/php | Located in ./tests/PhpUnit
`php -f ./tests/phptestgen.php LocA` | Located in ./tests/LocA | Located in ./tests/PhpUnit
`php -f ./tests/phptestgen.php LocA LocB` | Located in ./tests/LocA | Located in ./tests/LocB
`php -f ./tests/phptestgen.php LocA multi` | Located in ./tests/LocA | Located in ./tests/php*.* with customizations.

Any of the above with an additional PHPUnit option given as X.Y.Z will write
files as specified above with customization.
When PHPUnit version is <  4.8.28, tests built as Non-Ns Non-Th.
When PHPUnit vesrion is between, tests built as Ns Non-Th.
When PHPUnit version is >= 7.0, tests built as Ns Th.

# Related Software
[PHPUNIT](https://github.com/sebastianbergmann/phpunit) by @sebastianbergmann