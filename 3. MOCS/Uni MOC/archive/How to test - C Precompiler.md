---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-16T09:43
updated: 2026-02-16T09:44
---
## Build

Build manualy with: 
- `mkdir bin`
- `gcc -Iinclude src/main.c src/core/ArgumentParser.c src/core/FileConcatenator.c src/core/IdentifiersNameChecker.c src/core/IncludeFinder.c src/core/NextWord.c src/utils/Compare.c src/utils/Str.c src/utils/StringList.c -o bin/our_c_precompiler` 

Or use make: `make all`

## Prof Tests
1. `make test_prof_1`: `./bin/our_c_precompiler -v -i test/prof_tests/test1/test1.c`
2. `make test_prof_2`: `./bin/our_c_precompiler -v -i test/prof_tests/test2/test2.c` 

## Include Test
1. `make test_circular_includes`: `./bin/our_c_precompiler -v -i test/include_tests/circular_includes/f1.c`
2. `make test_ordered_includes`: `./bin/our_c_precompiler -v -i test/include_tests/ordered_includes/main.c`

## Parsing Tests
1. `make test_parsing_1`: `./bin/our_c_precompiler -v -i test/parsing_tests/array_test.c`
2. `make test_parsing_2`: `./bin/our_c_precompiler -v -i test/parsing_tests/comment_test.c`
3. `make test_parsing_3`: `./bin/our_c_precompiler -v -i test/parsing_tests/datatype_test.c`
4. `make test_parsing_4`: `./bin/our_c_precompiler -v -i test/parsing_tests/define_test.c`
5. `make test_parsing_5`: `./bin/our_c_precompiler -v -i test/parsing_tests/enum_test.c`
6. `make test_parsing_6`: `./bin/our_c_precompiler -v -i test/parsing_tests/typedef_test.c`

## Error Tests
1. `make error_test_1`: `./bin/our_c_precompiler -v -i test/error_tests/advanced_errors.c`
2. `make error_test_2`: `./bin/our_c_precompiler -v -i test/error_tests/double_function.c`
3. `make error_test_3`: `./bin/our_c_precompiler -v -i test/error_tests/enum_test1_errors.c`
4. `make error_test_4`: `./bin/our_c_precompiler -v -i test/error_tests/enum_test2_errors.c`
5. `make error_test_5`: `./bin/our_c_precompiler -v -i test/error_tests/many_errors.c`
6. `make error_test_6`: `./bin/our_c_precompiler -v -i test/error_tests/pointer_test.c`
7. `make error_test_7`: `./bin/our_c_precompiler -v -i test/error_tests/struct_test.c`
8. `make error_test_8`: `./bin/our_c_precompiler -v -i test/error_tests/variable_errors.c`